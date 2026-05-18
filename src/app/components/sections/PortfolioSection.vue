<script setup lang="ts">
import bg3 from '~/assets/bg3.png'

interface PortfolioItem {
  title: string
  category: string
  description: string
  stack: string[]
}

const project: PortfolioItem = {
  title: 'Nebulos',
  category: 'ERP',
  description: 'ERP com modulo de vendas interno para clientes, feito em Vue/Nuxt e Zig com framework proprio da empresa.',
  stack: ['Vue', 'Nuxt', 'Zig', 'Framework proprio']
}
</script>

<template>
  <section
    id="portfolio"
    class="relative section-spacious overflow-hidden"
  >
    <div class="section-backdrop">
      <img
        :src="bg3"
        alt="Campo estelar com rastros dinâmicos"
        loading="lazy"
        decoding="async"
        fetchpriority="low"
      >
      <div class="section-overlay-soft" />
    </div>

    <div class="section-shell relative z-10">
      <div class="fade-reveal max-w-2xl mb-10 md:mb-12">
        <UBadge
          label="PORTFÓLIO"
          color="primary"
          variant="soft"
          class="w-fit"
        />
        <h2 class="display-font text-3xl md:text-5xl mt-3">
          Projetos que geram impacto
        </h2>
      </div>

      <div class="fade-reveal max-w-4xl">
        <UCard class="service-card premium-panel overflow-hidden">
          <div class="h-48 rounded-xl relative overflow-hidden mb-4 border border-white/10">
            <img
              :src="bg3"
              alt="Textura estelar"
              class="w-full h-full object-cover"
              loading="lazy"
              decoding="async"
              fetchpriority="low"
            >
            <div class="media-mask" />
            <div class="absolute inset-0 bg-[radial-gradient(circle_at_18%_20%,rgba(255,255,255,0.28),transparent_40%),radial-gradient(circle_at_78%_80%,rgba(11,15,26,0.45),transparent_45%)]" />
            <div class="absolute inset-0 grid place-items-center">
              <UBadge
                :label="project.category"
                color="neutral"
                variant="solid"
              />
            </div>
          </div>

          <h3 class="text-lg font-semibold">
            {{ project.title }}
          </h3>
          <p class="text-sm text-[color:var(--text-soft)] mt-2 leading-relaxed">
            {{ project.description }}
          </p>
          <div class="flex flex-wrap gap-2 mt-4">
            <UBadge
              v-for="tech in project.stack"
              :key="`${project.title}-${tech}`"
              :label="tech"
              color="neutral"
              variant="soft"
              size="sm"
            />
          </div>
        </UCard>
      </div>
    </div>
  </section>
</template>
