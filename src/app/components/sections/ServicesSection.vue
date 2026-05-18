<script setup lang="ts">
const services = [
  {
    title: 'Desenvolvimento Web',
    description: 'Plataformas modernas, escaláveis e orientadas a performance para acelerar resultados digitais.',
    icon: 'i-lucide-layout-template'
  },
  {
    title: 'Aplicações Mobile',
    description: 'Experiências nativas e híbridas com foco em usabilidade, retenção e velocidade de entrega.',
    icon: 'i-lucide-smartphone'
  },
  {
    title: 'Sistemas ERP',
    description: 'Integração de processos, dados e operações com visão unificada para decisões estratégicas.',
    icon: 'i-lucide-network'
  }
]
</script>

<template>
  <section
    id="servicos"
    class="relative section-spacious"
  >
    <div class="section-divider" />

    <div class="section-shell relative z-10">
      <div class="fade-reveal section-heading">
        <UBadge
          label="SERVIÇOS"
          color="primary"
          variant="soft"
          class="w-fit"
        />
        <h2 class="display-font text-3xl md:text-5xl mt-3">
          Soluções completas para o seu negócio
        </h2>
        <p class="text-[color:var(--text-soft)] mt-4 leading-relaxed">
          Soluções ponta a ponta com o padrão premium da QuantumOrbit para produtos, operações e inovação contínua.
        </p>
      </div>

      <div class="grid sm:grid-cols-2 xl:grid-cols-3 gap-4 md:gap-5">
        <UCard
          v-for="service in services"
          :key="service.title"
          class="fade-reveal service-card premium-panel group"
        >
          <template #header>
            <div class="w-11 h-11 rounded-xl grid place-items-center bg-[var(--gradient-secondary)] text-white shadow-[0_0_26px_rgba(30,144,255,0.35)]">
              <UIcon
                :name="service.icon"
                class="size-5"
              />
            </div>
          </template>

          <h3 class="text-lg font-semibold">
            {{ service.title }}
          </h3>
          <p class="text-sm text-[color:var(--text-soft)] mt-2 leading-relaxed">
            {{ service.description }}
          </p>
          <div class="mt-4 text-xs uppercase tracking-[0.15em] text-cyan-500 dark:text-cyan-300">
            Performance + Escala
          </div>
        </UCard>
      </div>
    </div>
  </section>
</template>
