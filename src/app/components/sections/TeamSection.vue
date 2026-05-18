<script setup lang="ts">
import bg2 from '~/assets/bg2.png'

interface TeamMember {
  name: string
  role: string
  bio: string
  skills: string[]
  socials: { label: string, href: string }[]
  projects: string[]
}

const members: TeamMember[] = [
  {
    name: 'Anderson Felipe',
    role: 'Arquiteto de Software e Desenvolvedor',
    bio: 'Responsavel pela arquitetura de software e pelo desenvolvimento de solucoes robustas, escalaveis e orientadas a performance.',
    skills: ['Arquitetura de Software', 'Backend', 'Frontend'],
    socials: [
      { label: 'E-mail', href: 'mailto:developer.anderson@spatialducks.com.br' }
    ],
    projects: []
  },
  {
    name: 'Raphael Esteves',
    role: 'Desenvolvedor',
    bio: 'Focado em construir interfaces modernas e experiências digitais fluidas, com atenção à qualidade de entrega.',
    skills: ['Frontend', 'Integrações', 'UX de Produto'],
    socials: [
      { label: 'E-mail', href: 'mailto:developer.rapdos@spatialducks.com.br' }
    ],
    projects: []
  }
]

const selectedMember = ref<TeamMember | null>(null)
const isModalOpen = ref(false)

async function openMember(member: TeamMember) {
  selectedMember.value = member
  await nextTick()
  isModalOpen.value = true
}

watch(isModalOpen, (isOpen) => {
  if (!isOpen) {
    selectedMember.value = null
  }
})
</script>

<template>
  <section
    id="time"
    class="relative section-spacious overflow-hidden"
  >
    <div class="section-divider" />
    <div class="section-backdrop opacity-45">
      <img
        :src="bg2"
        alt="Anéis orbitais"
        class="object-right"
        loading="lazy"
        decoding="async"
        fetchpriority="low"
      >
      <div class="section-overlay-soft" />
    </div>

    <div class="section-shell relative z-10">
      <div class="fade-reveal max-w-2xl mb-10 md:mb-12">
        <UBadge
          label="TIME"
          color="primary"
          variant="soft"
          class="w-fit"
        />
        <h2 class="display-font text-3xl md:text-5xl mt-3">
          Desenvolvedores que constroem o futuro
        </h2>
      </div>

      <div class="grid md:grid-cols-2 gap-4 md:gap-5">
        <UCard
          v-for="member in members"
          :key="member.name"
          class="fade-reveal service-card premium-panel"
        >
          <div class="w-14 h-14 rounded-2xl grid place-items-center text-white font-bold text-lg animated-gradient">
            {{ member.name.split(' ').map(part => part[0]).join('').slice(0, 2) }}
          </div>
          <h3 class="font-semibold text-lg mt-4">
            {{ member.name }}
          </h3>
          <p class="text-sm text-cyan-500 dark:text-cyan-300 mt-1">
            {{ member.role }}
          </p>
          <p class="text-sm text-[color:var(--text-soft)] mt-3 leading-relaxed">
            {{ member.bio }}
          </p>
          <UButton
            label="Ver detalhes"
            variant="soft"
            color="neutral"
            class="mt-5"
            @click.stop.prevent="openMember(member)"
          />
        </UCard>
      </div>

      <UModal
        v-model:open="isModalOpen"
        :ui="{ content: 'max-w-2xl' }"
      >
        <template #content="{ close }">
          <div
            v-if="selectedMember"
            class="premium-panel rounded-3xl border border-[color:var(--border)]/80 p-6 md:p-7 space-y-5"
          >
            <div class="flex items-start justify-between gap-4">
              <div>
                <h3 class="display-font text-2xl">
                  {{ selectedMember.name }}
                </h3>
                <p class="text-sm text-cyan-500 dark:text-cyan-300 mt-1">
                  {{ selectedMember.role }}
                </p>
              </div>

              <UButton
                icon="i-lucide-x"
                color="neutral"
                variant="ghost"
                aria-label="Fechar modal"
                @click="close"
              />
            </div>

            <p class="text-sm text-[color:var(--text-soft)] leading-relaxed">
              {{ selectedMember.bio }}
            </p>

            <div>
              <p class="text-xs tracking-[0.15em] text-[color:var(--text-soft)] uppercase">
                Habilidades
              </p>
              <div class="flex flex-wrap gap-2 mt-2">
                <UBadge
                  v-for="skill in selectedMember.skills"
                  :key="`${selectedMember.name}-${skill}`"
                  :label="skill"
                  color="neutral"
                  variant="soft"
                />
              </div>
            </div>

            <div v-if="selectedMember.projects.length">
              <p class="text-xs tracking-[0.15em] text-[color:var(--text-soft)] uppercase">
                Projetos
              </p>
              <ul class="mt-2 space-y-1 text-sm text-[color:var(--text-soft)]">
                <li
                  v-for="project in selectedMember.projects"
                  :key="project"
                >
                  • {{ project }}
                </li>
              </ul>
            </div>

            <div v-if="selectedMember.socials.length">
              <p class="text-xs tracking-[0.15em] text-[color:var(--text-soft)] uppercase">
                Redes
              </p>
              <div class="flex flex-wrap gap-2 mt-2">
                <UButton
                  v-for="social in selectedMember.socials"
                  :key="`${selectedMember.name}-${social.label}`"
                  :label="social.label"
                  :to="social.href"
                  target="_blank"
                  color="neutral"
                  variant="soft"
                  size="sm"
                />
              </div>
            </div>
          </div>
        </template>
      </UModal>
    </div>
  </section>
</template>
