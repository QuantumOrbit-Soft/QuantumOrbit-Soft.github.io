<script setup lang="ts">
import bg5 from '~/assets/bg5.png'

const form = reactive({
  nome: '',
  email: '',
  empresa: '',
  mensagem: ''
})

const FIELD_LIMITS = {
  nome: { min: 2, max: 80 },
  email: { max: 120 },
  empresa: { max: 100 },
  mensagem: { min: 10, max: 2000 }
} as const

const formErrors = reactive({
  nome: '',
  email: '',
  empresa: '',
  mensagem: ''
})

const fallbackMessage = ref('')
const honeypot = ref('')
const isSubmitting = ref(false)
const lastSubmitAt = ref(0)

const SUBMIT_COOLDOWN_MS = 12_000

const inputUi = {
  root: 'w-full',
  base: 'h-12 rounded-xl border border-[color:var(--border)]/90 bg-white/88 dark:bg-[color:var(--surface)]/72 px-4 text-sm text-[color:var(--text-main)] placeholder:text-[color:var(--text-soft)]/80 shadow-sm shadow-black/4 dark:shadow-none focus-visible:ring-2 focus-visible:ring-[color:var(--cyan)]/30 focus-visible:border-[color:var(--cyan)]/55 transition-colors'
}

const textareaUi = {
  root: 'w-full',
  base: 'rounded-xl border border-[color:var(--border)]/90 bg-white/88 dark:bg-[color:var(--surface)]/72 px-4 py-3 text-sm text-[color:var(--text-main)] placeholder:text-[color:var(--text-soft)]/80 shadow-sm shadow-black/4 dark:shadow-none focus-visible:ring-2 focus-visible:ring-[color:var(--cyan)]/30 focus-visible:border-[color:var(--cyan)]/55 transition-colors'
}

const cardUi = {
  root: 'contact-form-card rounded-3xl border border-[color:var(--border)]/85',
  body: 'p-6 md:p-7'
}

const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/

function stripControlChars(value: string) {
  return [...value]
    .filter((char) => {
      const code = char.charCodeAt(0)
      return code >= 32 || code === 9 || code === 10 || code === 13
    })
    .join('')
}

function sanitizeText(value: string) {
  return stripControlChars(value)
    .replace(/<\/?\s*script\b[^>]*>/gi, ' ')
    .replace(/<[^>]*>/g, ' ')
    .replace(/[<>]/g, ' ')
    .replace(/\s+/g, ' ')
    .trim()
}

function sanitizeMessage(value: string) {
  return stripControlChars(value)
    .replace(/<\/?\s*script\b[^>]*>/gi, ' ')
    .replace(/<[^>]*>/g, ' ')
    .replace(/[<>]/g, ' ')
    .replace(/\r\n?/g, '\n')
    .replace(/\t/g, ' ')
    .replace(/[ \f\v]+/g, ' ')
    .replace(/\n{3,}/g, '\n\n')
    .trim()
}

function validateForm() {
  const sanitized = {
    nome: sanitizeText(form.nome),
    email: sanitizeText(form.email).toLowerCase(),
    empresa: sanitizeText(form.empresa),
    mensagem: sanitizeMessage(form.mensagem)
  }

  formErrors.nome = ''
  formErrors.email = ''
  formErrors.empresa = ''
  formErrors.mensagem = ''

  if (!sanitized.nome) {
    formErrors.nome = 'Informe seu nome.'
  } else if (sanitized.nome.length < FIELD_LIMITS.nome.min) {
    formErrors.nome = `O nome deve ter pelo menos ${FIELD_LIMITS.nome.min} caracteres.`
  } else if (sanitized.nome.length > FIELD_LIMITS.nome.max) {
    formErrors.nome = `O nome deve ter no máximo ${FIELD_LIMITS.nome.max} caracteres.`
  }

  if (!sanitized.email) {
    formErrors.email = 'Informe seu e-mail.'
  } else if (sanitized.email.length > FIELD_LIMITS.email.max) {
    formErrors.email = `O e-mail deve ter no máximo ${FIELD_LIMITS.email.max} caracteres.`
  } else if (!emailPattern.test(sanitized.email)) {
    formErrors.email = 'Informe um e-mail válido.'
  }

  if (sanitized.empresa.length > FIELD_LIMITS.empresa.max) {
    formErrors.empresa = `A empresa deve ter no máximo ${FIELD_LIMITS.empresa.max} caracteres.`
  }

  if (!sanitized.mensagem) {
    formErrors.mensagem = 'Informe sua mensagem.'
  } else if (sanitized.mensagem.length < FIELD_LIMITS.mensagem.min) {
    formErrors.mensagem = `A mensagem deve ter pelo menos ${FIELD_LIMITS.mensagem.min} caracteres.`
  } else if (sanitized.mensagem.length > FIELD_LIMITS.mensagem.max) {
    formErrors.mensagem = `A mensagem deve ter no máximo ${FIELD_LIMITS.mensagem.max} caracteres.`
  }

  const hasErrors = Object.values(formErrors).some(Boolean)
  return { sanitized, isValid: !hasErrors }
}

function submitForm() {
  if (isSubmitting.value) {
    return
  }

  if (honeypot.value.trim()) {
    fallbackMessage.value = 'Não foi possível processar o envio. Tente novamente.'
    return
  }

  const now = Date.now()
  const elapsedSinceLastSubmit = now - lastSubmitAt.value

  if (elapsedSinceLastSubmit < SUBMIT_COOLDOWN_MS) {
    const waitSeconds = Math.ceil((SUBMIT_COOLDOWN_MS - elapsedSinceLastSubmit) / 1000)
    fallbackMessage.value = `Aguarde ${waitSeconds}s antes de enviar novamente.`
    return
  }

  isSubmitting.value = true

  const { sanitized, isValid } = validateForm()

  if (!isValid) {
    fallbackMessage.value = ''
    isSubmitting.value = false
    return
  }

  form.nome = sanitized.nome
  form.email = sanitized.email
  form.empresa = sanitized.empresa
  form.mensagem = sanitized.mensagem

  const subjectParts = ['Contato via site QuantumOrbit']

  if (sanitized.empresa) {
    subjectParts.push(`(${sanitized.empresa})`)
  }

  const bodyLines = [
    `Nome: ${sanitized.nome}`,
    `E-mail: ${sanitized.email}`,
    sanitized.empresa ? `Empresa: ${sanitized.empresa}` : null,
    '',
    'Mensagem:',
    sanitized.mensagem
  ].filter(Boolean)

  const mailtoUrl = `mailto:contato@spatialducks.com.br?subject=${encodeURIComponent(subjectParts.join(' '))}&body=${encodeURIComponent(bodyLines.join('\n'))}`

  if (typeof window !== 'undefined') {
    lastSubmitAt.value = now
    window.location.href = mailtoUrl
    fallbackMessage.value = 'Abrimos seu aplicativo de e-mail com a mensagem preenchida. Envie por lá para concluir o contato.'
  }

  setTimeout(() => {
    isSubmitting.value = false
  }, 800)
}
</script>

<template>
  <section
    id="contato"
    class="relative section-spacious overflow-hidden"
  >
    <div class="section-backdrop">
      <img
        :src="bg5"
        alt="Planeta com anéis orbitais"
        class="object-right"
      >
      <div class="section-overlay-soft" />
    </div>

    <div class="section-shell relative z-10">
      <div class="grid lg:grid-cols-2 gap-6 md:gap-8 items-stretch">
        <div class="fade-reveal premium-panel rounded-3xl border border-[color:var(--border)]/80 p-6 md:p-8 overflow-hidden">
          <div class="absolute inset-0 opacity-1 pointer-events-none">
            <img
              :src="bg5"
              alt="Visual orbital"
              class="w-full h-full object-cover object-right"
            >
            <div class="media-mask" />
          </div>

          <div class="relative z-10">
            <UBadge
              label="CONTATO"
              color="primary"
              variant="soft"
              class="w-fit"
            />
            <h2 class="display-font text-3xl md:text-5xl mt-3">
              Vamos construir seu próximo salto tecnológico
            </h2>
            <p class="text-[color:var(--text-soft)] mt-4 leading-relaxed">
              Fale com a QuantumOrbit para desenhar uma solução sob medida para sua operação.
            </p>

            <div class="mt-6 space-y-3 text-sm text-[color:var(--text-soft)]">
              <p class="flex gap-2">
                <strong class="text-[color:var(--text-main)]">E-mail:</strong> contato@spatialducks.com.br
              </p>
              <p class="flex gap-2">
                <strong class="text-[color:var(--text-main)]">Telefone:</strong>
                <a
                  href="tel:+5515997952170"
                  class="hover:text-[color:var(--text-main)] transition-colors"
                >+55 15 99795-2170</a>
              </p>
              <p class="flex gap-2">
                <strong class="text-[color:var(--text-main)]">Instagram:</strong>
                <a
                  href="https://www.instagram.com/quantumorbitsoft/"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="hover:text-[color:var(--text-main)] transition-colors"
                >@quantumorbitsoft</a>
              </p>
              <p class="flex gap-2">
                <strong class="text-[color:var(--text-main)]">Endereço:</strong> São Paulo • Brasil
              </p>
            </div>
          </div>
        </div>

        <UCard
          class="fade-reveal service-card premium-panel opacity-1"
          :ui="cardUi"
        >
          <div class="mb-6 space-y-2">
            <p class="text-xs font-semibold tracking-[0.16em] text-[color:var(--text-soft)] uppercase">
              Formulário de contato
            </p>
            <p class="text-sm text-[color:var(--text-soft)] leading-relaxed">
              Preencha os campos e abriremos seu e-mail com a mensagem pronta.
            </p>
          </div>

          <form
            class="contact-form space-y-4"
            @submit.prevent="submitForm"
          >
            <input
              v-model="honeypot"
              type="text"
              name="website"
              autocomplete="off"
              tabindex="-1"
              aria-hidden="true"
              class="hp-field"
            >
            <div class="field-group">
              <label class="field-label">Nome</label>
              <UInput
                v-model="form.nome"
                placeholder="Seu nome"
                :ui="inputUi"
                autocomplete="name"
                :maxlength="FIELD_LIMITS.nome.max"
                required
              />
              <p
                v-if="formErrors.nome"
                class="field-error"
              >
                {{ formErrors.nome }}
              </p>
            </div>
            <div class="field-group">
              <label class="field-label">E-mail</label>
              <UInput
                v-model="form.email"
                type="email"
                placeholder="Seu e-mail"
                :ui="inputUi"
                autocomplete="email"
                inputmode="email"
                :maxlength="FIELD_LIMITS.email.max"
                required
              />
              <p
                v-if="formErrors.email"
                class="field-error"
              >
                {{ formErrors.email }}
              </p>
            </div>
            <div class="field-group">
              <label class="field-label">Empresa</label>
              <UInput
                v-model="form.empresa"
                placeholder="Empresa"
                :ui="inputUi"
                autocomplete="organization"
                :maxlength="FIELD_LIMITS.empresa.max"
              />
              <p
                v-if="formErrors.empresa"
                class="field-error"
              >
                {{ formErrors.empresa }}
              </p>
            </div>
            <div class="field-group">
              <label class="field-label">Mensagem</label>
              <UTextarea
                v-model="form.mensagem"
                placeholder="Descreva o desafio do seu projeto"
                :rows="5"
                :ui="textareaUi"
                autocomplete="off"
                :maxlength="FIELD_LIMITS.mensagem.max"
                required
              />
              <p
                v-if="formErrors.mensagem"
                class="field-error"
              >
                {{ formErrors.mensagem }}
              </p>
            </div>
            <UButton
              type="submit"
              label="Enviar mensagem"
              size="lg"
              class="animated-gradient text-white border-0 mt-2"
              :loading="isSubmitting"
              :disabled="isSubmitting"
              :ui="{ base: 'justify-center px-6 h-12 w-full md:w-auto md:min-w-48' }"
            />
          </form>

          <p
            v-if="fallbackMessage"
            class="text-sm text-[color:var(--text-soft)] mt-4"
          >
            {{ fallbackMessage }}
          </p>
        </UCard>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hp-field {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  border: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  clip-path: inset(50%);
  white-space: nowrap;
}

.field-group {
  display: grid;
  gap: 0.45rem;
}

.field-label {
  font-size: 0.8rem;
  line-height: 1.2;
  color: var(--text-soft);
  font-weight: 600;
  letter-spacing: 0.01em;
}

.field-error {
  font-size: 0.78rem;
  line-height: 1.3;
  color: #fca5a5;
}
</style>
