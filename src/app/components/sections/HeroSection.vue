<script setup lang="ts">
import logo from '~/assets/logo_trasparent.png'
import bg1 from '~/assets/bg1.png'
import bg2 from '~/assets/bg2.png'
</script>

<template>
  <section
    id="home"
    class="relative pt-34 pb-20 md:pb-24 overflow-hidden"
  >
    <div class="section-backdrop">
      <img
        :src="bg1"
        alt="Horizonte espacial"
        class="object-center"
        loading="eager"
        decoding="async"
        fetchpriority="high"
      >
      <div class="section-overlay-dark" />
    </div>

    <div class="section-shell relative z-10 grid lg:grid-cols-2 gap-10 md:gap-14 items-center">
      <div class="fade-reveal space-y-7">
        <UBadge
          label="SOFTWARE • SISTEMAS"
          color="primary"
          variant="soft"
          class="w-fit"
        />
        <h1 class="display-font text-4xl md:text-6xl font-extrabold leading-tight max-w-2xl">
          Tecnologia que <span class="gradient-text">Impulsiona o Futuro</span>
        </h1>
        <p class="text-base md:text-lg text-slate-800 dark:text-[color:var(--text-soft)] max-w-xl leading-relaxed">
          Na QuantumOrbit, criamos plataformas digitais de alta performance para acelerar operações, experiência do cliente e inteligência de negócio.
        </p>
        <div class="flex flex-wrap gap-3 pt-1">
          <UButton
            label="Conheça nossos projetos"
            to="#portfolio"
            size="xl"
            class="animated-gradient text-white border-0"
          />
          <UButton
            label="Fale conosco"
            to="#contato"
            size="xl"
            color="neutral"
            variant="soft"
            class="text-slate-900 dark:text-white border border-black/10 dark:border-white/15"
          />
        </div>
      </div>

      <div class="fade-reveal relative min-h-[360px] grid place-items-center">
        <div class="absolute inset-x-4 md:inset-x-8 h-[88%] rounded-[2rem] overflow-hidden border border-white/10">
          <img
            :src="bg2"
            alt="Anéis orbitais"
            class="w-full h-full object-cover"
            loading="eager"
            decoding="async"
            fetchpriority="low"
          >
          <div class="media-mask" />
        </div>
        <div class="absolute w-[360px] h-[360px] rounded-full blur-3xl bg-[radial-gradient(circle,_rgba(138,43,226,0.34),_rgba(30,144,255,0.08)_56%,_transparent_82%)]" />
        <div class="relative w-[330px] h-[330px] drift">
          <div class="absolute inset-[5.4rem] grid place-items-center z-20 pointer-events-none">
            <img
              :src="logo"
              alt="Logo QuantumOrbit"
              class="w-40 h-40 object-contain drop-shadow-[0_8px_24px_rgba(108,59,255,0.28)]"
            >
          </div>

          <div class="absolute inset-0 orbital-spin">
            <div class="orbital-dot orbital-dot-lg top-[7%] left-1/2 -translate-x-1/2" />
          </div>

          <div class="absolute inset-9 orbital-spin-reverse">
            <div class="orbital-dot orbital-dot-md top-[3%] left-1/2 -translate-x-1/2" />
          </div>

          <div class="absolute inset-[4.2rem] orbital-spin">
            <div class="orbital-dot orbital-dot-sm top-[6%] left-1/2 -translate-x-1/2" />
          </div>

          <div class="absolute inset-0 orbital-tilt">
            <div class="absolute top-[17%] right-[22%] w-3 h-3 rounded-full bg-cyan-200/90 shadow-[0_0_16px_rgba(0,212,255,0.65)]" />
            <div class="absolute bottom-[19%] left-[20%] w-2 h-2 rounded-full bg-violet-200/80 shadow-[0_0_14px_rgba(138,43,226,0.55)]" />
          </div>

          <div class="absolute inset-0 pointer-events-none">
            <div class="absolute inset-0 rounded-full border border-white/40 dark:border-white/30" />
            <div class="absolute inset-9 rounded-full border border-white/34 dark:border-white/24" />
            <div class="absolute inset-[4.2rem] rounded-full border border-white/22 dark:border-white/18" />
            <div class="absolute inset-[1.1rem] rounded-full border border-[color:var(--cyan)]/24" />
            <div class="absolute inset-[1.1rem] rounded-full border border-[color:var(--purple-primary)]/15 orbital-tilt" />
          </div>

          <div class="absolute inset-0 orbital-tilt-reverse pointer-events-none">
            <div class="absolute top-[14%] left-1/2 -translate-x-1/2 w-10 h-10 rounded-full border border-cyan-100/70 dark:border-cyan-200/65 bg-white/12 dark:bg-cyan-100/8" />
            <div class="absolute bottom-[13%] left-[16%] w-8 h-8 rounded-full border border-violet-100/70 dark:border-violet-200/65 bg-white/10 dark:bg-violet-100/8" />
          </div>

          <div class="absolute inset-0 orbital-spin-reverse pointer-events-none">
            <div class="absolute top-[6%] right-[17%] w-12 h-12 rounded-full border border-white/55 dark:border-white/40 bg-white/16 dark:bg-white/10 shadow-[0_0_22px_rgba(0,212,255,0.28)]" />
            <div class="absolute bottom-[8%] right-[30%] w-5 h-5 rounded-full border border-white/45 dark:border-white/30 bg-white/12 dark:bg-white/8" />
          </div>

          <div class="absolute inset-0">
            <div class="absolute inset-[34%] rounded-full bg-[radial-gradient(circle,_rgba(255,255,255,0.32),_transparent_72%)] dark:bg-[radial-gradient(circle,_rgba(248,250,252,0.14),_transparent_72%)]" />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
