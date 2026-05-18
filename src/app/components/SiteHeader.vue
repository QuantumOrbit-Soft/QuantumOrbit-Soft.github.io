<script setup lang="ts">
import logo from '~/assets/logo_trasparent.png'

const links = [
  { label: 'Home', to: '#home' },
  { label: 'About', to: '#sobre' },
  { label: 'Portfolio', to: '#portfolio' },
  { label: 'Team', to: '#time' },
  { label: 'Contact', to: '#contato' }
]

const mobileOpen = ref(false)
</script>

<template>
  <header class="fixed top-0 inset-x-0 z-50 border-b border-[color:var(--border)]/70 glass">
    <nav class="section-shell h-18 flex items-center justify-between gap-3">
      <a
        href="#"
        class="flex items-center"
      >
        <img
          :src="logo"
          alt="Logo QuantumOrbit"
          class="w-54 h-54 object-contain"
        >
      </a>

      <ul class="hidden md:flex items-center gap-2 text-sm text-[color:var(--text-soft)]">
        <li
          v-for="item in links"
          :key="item.label"
        >
          <a
            :href="item.to"
            class="nav-link"
          >{{ item.label }}</a>
        </li>
      </ul>

      <div class="hidden md:flex items-center gap-2">
        <UButton
          label="Fale conosco"
          to="#contato"
          class="animated-gradient text-white border-0"
        />
      </div>

      <div class="md:hidden flex items-center gap-1">
        <UButton
          color="neutral"
          variant="soft"
          icon="i-lucide-menu"
          aria-label="Abrir menu"
          @click="mobileOpen = !mobileOpen"
        />
      </div>
    </nav>

    <Transition name="fade">
      <div
        v-if="mobileOpen"
        class="md:hidden section-shell pb-4"
      >
        <div class="glass rounded-2xl p-4 flex flex-col gap-3">
          <a
            v-for="item in links"
            :key="item.label"
            :href="item.to"
            class="text-sm text-[color:var(--text-soft)] hover:text-[color:var(--text-main)]"
            @click="mobileOpen = false"
          >
            {{ item.label }}
          </a>
          <UButton
            label="Fale conosco"
            to="#contato"
            class="animated-gradient text-white border-0"
            @click="mobileOpen = false"
          />
        </div>
      </div>
    </Transition>
  </header>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.nav-link {
  position: relative;
  display: inline-flex;
  align-items: center;
  padding: 0.44rem 0.82rem;
  border-radius: 999px;
  color: var(--text-soft);
  border: 1px solid transparent;
  transition: color 220ms ease, border-color 220ms ease, background-color 220ms ease, box-shadow 220ms ease;
}

.nav-link:hover {
  color: var(--text-main);
  border-color: color-mix(in srgb, var(--cyan) 24%, var(--border));
  background: color-mix(in srgb, var(--surface) 74%, white 26%);
  box-shadow: 0 0 0 1px color-mix(in srgb, var(--cyan) 16%, transparent);
}

.dark .nav-link:hover {
  background: color-mix(in srgb, var(--surface) 82%, transparent);
}
</style>
