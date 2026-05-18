<script setup lang="ts">
useHead({
  htmlAttrs: {
    lang: 'pt-BR'
  },
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  script: [
    {
      type: 'application/ld+json',
      innerHTML: JSON.stringify({
        '@context': 'https://schema.org',
        '@graph': [
          {
            '@type': 'Organization',
            'name': 'QuantumOrbit',
            'alternateName': 'SpatialDucks',
            'description':
              'Empresa de desenvolvimento de software sob medida para web, mobile, sistemas corporativos e ERP.',
            'knowsAbout': ['Desenvolvimento Web', 'Aplicativos Mobile', 'Sistemas ERP', 'Sistemas Corporativos']
          },
          {
            '@type': 'Service',
            'serviceType': 'Desenvolvimento de software sob medida',
            'provider': {
              '@type': 'Organization',
              'name': 'QuantumOrbit'
            },
            'areaServed': 'BR',
            'offers': {
              '@type': 'Offer',
              'category': 'Desenvolvimento Web, Mobile e Sistemas ERP'
            }
          }
        ]
      })
    }
  ],
  link: [
    { rel: 'icon', type: 'image/svg+xml', href: '/favicon.svg' },
    { rel: 'alternate icon', type: 'image/x-icon', href: '/favicon.ico' }
  ]
})

useSeoMeta({
  title: 'QuantumOrbit • Desenvolvimento de Software, ERP, Web e Mobile',
  description:
    'Software sob medida para empresas que exigem excelência técnica em sistemas ERP, plataformas web e aplicativos mobile.',
  ogTitle: 'QuantumOrbit • Software sob medida para negócios digitais',
  ogDescription:
    'Projetamos e desenvolvemos sistemas ERP, aplicações web e mobile com foco em performance, escala e resultado.',
  ogType: 'website',
  ogSiteName: 'QuantumOrbit',
  twitterCard: 'summary_large_image',
  twitterTitle: 'QuantumOrbit • Desenvolvimento de Software e Sistemas',
  twitterDescription:
    'Soluções premium em software sob medida: ERP, sistemas corporativos, web e mobile para empresas em crescimento.',
  robots: 'index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1',
  author: 'QuantumOrbit / SpatialDucks',
  keywords:
    'desenvolvimento de software, software sob medida, sistemas ERP, desenvolvimento web, aplicativos mobile, sistemas corporativos, transformação digital'
})
</script>

<template>
  <UApp>
    <div class="site-bg" />
    <SiteHeader />
    <main>
      <NuxtPage />
    </main>
    <SiteFooter />
  </UApp>
</template>
