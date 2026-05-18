<script setup lang="ts">
import AboutSection from '~/components/sections/AboutSection.vue'
import ContactSection from '~/components/sections/ContactSection.vue'
import HeroSection from '~/components/sections/HeroSection.vue'
import PortfolioSection from '~/components/sections/PortfolioSection.vue'
import ServicesSection from '~/components/sections/ServicesSection.vue'
import TeamSection from '~/components/sections/TeamSection.vue'

let observer: IntersectionObserver | null = null

onMounted(() => {
  const root = document.documentElement

  const revealOnLoad = () => {
    document.querySelectorAll<HTMLElement>('.fade-reveal').forEach((element) => {
      const { top } = element.getBoundingClientRect()

      if (top <= window.innerHeight * 0.95) {
        element.classList.add('is-visible')
      }
    })
  }

  revealOnLoad()
  root.classList.add('reveal-enhanced')

  observer = new IntersectionObserver((entries) => {
    for (const entry of entries) {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible')
      }
    }
  }, { threshold: 0.08, rootMargin: '0px 0px -8% 0px' })

  document.querySelectorAll('.fade-reveal').forEach((element) => {
    observer?.observe(element)
  })
})

onBeforeUnmount(() => {
  document.documentElement.classList.remove('reveal-enhanced')
  observer?.disconnect()
})
</script>

<template>
  <div class="pb-8">
    <HeroSection />
    <ServicesSection />
    <PortfolioSection />
    <AboutSection />
    <TeamSection />
    <ContactSection />
  </div>
</template>
