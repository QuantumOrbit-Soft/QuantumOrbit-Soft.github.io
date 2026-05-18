<script setup lang="ts">
import logo from '~/assets/logo_trasparent.png'
import bg4 from '~/assets/bg4.png'

const pillars = [
  {
    title: 'Missão',
    description: 'Transformar desafios complexos em soluções digitais seguras, rápidas e orientadas a valor.'
  },
  {
    title: 'Visão',
    description: 'Ser referência em tecnologia aplicada, conectando estratégia, produto e inteligência artificial.'
  },
  {
    title: 'Valores',
    description: 'Excelência técnica, transparência radical, parceria contínua e evolução baseada em dados.'
  }
]
</script>

<template>
  <section
    id="sobre"
    class="relative section-spacious overflow-hidden"
  >
    <div class="section-backdrop">
      <img
        :src="bg4"
        alt="Ondas digitais abstratas"
        loading="lazy"
        decoding="async"
        fetchpriority="low"
      >
      <div class="section-overlay-soft" />
    </div>

    <div class="section-shell relative z-10">
      <div class="grid lg:grid-cols-2 gap-6 md:gap-8 items-stretch">
        <div class="fade-reveal premium-panel p-6 md:p-8">
          <UBadge
            label="SOBRE"
            color="primary"
            variant="soft"
            class="w-fit"
          />
          <h2 class="display-font text-3xl md:text-5xl mt-3">
            Engenharia digital com visão de negócio
          </h2>
          <p class="text-[color:var(--text-soft)] mt-4 leading-relaxed">
            A QuantumOrbit combina arquitetura moderna, design de produto e automação inteligente para criar ecossistemas
            tecnológicos preparados para o próximo ciclo de crescimento.
          </p>

          <div class="mt-6 flex items-center gap-4 rounded-2xl p-4 border border-[color:var(--border)]/70 bg-[color:var(--surface)]/55">
            <img
              :src="logo"
              alt="QuantumOrbit"
              class="w-14 h-14 object-contain"
            >
            <p class="text-sm text-[color:var(--text-soft)]">
              Produto, plataforma e dados em uma operação integrada para empresas em expansão.
            </p>
          </div>

          <div class="relative mt-6 rounded-2xl overflow-hidden border border-white/10 h-44 hidden md:block">
            <img
              :src="bg4"
              alt="Painel tecnológico"
              class="w-full h-full object-cover"
              loading="lazy"
              decoding="async"
              fetchpriority="low"
            >
            <div class="media-mask" />
          </div>
        </div>

        <div class="space-y-4 md:space-y-5">
          <UCard
            v-for="pillar in pillars"
            :key="pillar.title"
            class="fade-reveal service-card premium-panel"
          >
            <h3 class="font-semibold text-lg">
              {{ pillar.title }}
            </h3>
            <p class="text-sm text-[color:var(--text-soft)] mt-2 leading-relaxed">
              {{ pillar.description }}
            </p>
          </UCard>
        </div>
      </div>
    </div>
  </section>
</template>
