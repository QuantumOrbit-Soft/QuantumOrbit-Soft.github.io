<template>
  <footer class="border-t border-[color:var(--border)]/70 mt-20">
    <div class="section-shell py-8 flex flex-col md:flex-row md:items-center md:justify-between gap-3 text-sm text-[color:var(--text-soft)]">
      <p>© {{ new Date().getFullYear() }} QuantumOrbit. Todos os direitos reservados.</p>
      <div class="flex items-center gap-4">
        <a
          href="#home"
          class="hover:text-[color:var(--text-main)]"
        >Home</a>
        <a
          href="#sobre"
          class="hover:text-[color:var(--text-main)]"
        >About</a>
        <a
          href="#portfolio"
          class="hover:text-[color:var(--text-main)]"
        >Portfolio</a>
        <a
          href="#time"
          class="hover:text-[color:var(--text-main)]"
        >Team</a>
        <a
          href="#contato"
          class="hover:text-[color:var(--text-main)]"
        >Contact</a>
      </div>
    </div>
  </footer>
</template>
