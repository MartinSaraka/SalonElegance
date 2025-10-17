<template>
  <div>
    <Navigation />
    
    <!-- Page Header -->
    <section class="pt-32 pb-16 bg-gradient-to-br from-secondary-800 to-secondary-900 text-white">
      <div class="container mx-auto px-4 text-center">
        <h1 class="font-serif text-4xl md:text-5xl font-bold mb-4">Ochrana osobných údajov</h1>
        <p class="text-lg text-gray-300 max-w-2xl mx-auto">
          Vaše súkromie je pre nás prioritou
        </p>
      </div>
    </section>

    <!-- Content -->
    <section class="py-20 bg-white">
      <div class="container mx-auto px-4 max-w-4xl">
        <div class="prose prose-lg max-w-none">
          <h2>1. Správca osobných údajov</h2>
          <p>
            Správcom vašich osobných údajov je Salon Elegance s.r.o., so sídlom Hlavná ulica 123, 811 01 Bratislava, IČO: 12345678.
          </p>

          <h2>2. Aké údaje zbierame</h2>
          <p>Pri rezervácii služby od vás môžeme požadovať:</p>
          <ul>
            <li>Meno a priezvisko</li>
            <li>Telefónne číslo</li>
            <li>Emailovú adresu</li>
            <li>Informácie o preferovaných službách</li>
          </ul>

          <h2>3. Účel spracovania</h2>
          <p>Vaše osobné údaje spracovávame za účelom:</p>
          <ul>
            <li>Spracovania a potvrdenia rezervácií</li>
            <li>Komunikácie ohľadom vašej návštevy</li>
            <li>Poskytnutia požadovaných služieb</li>
            <li>Zasielania marketingových informácií (so súhlasom)</li>
          </ul>

          <h2>4. Doba uchovávania</h2>
          <p>
            Vaše osobné údaje uchovávame po dobu nevyhnutnú na splnenie účelu, na ktorý boli získané, 
            alebo po dobu požadovanú zákonom.
          </p>

          <h2>5. Vaše práva</h2>
          <p>Máte právo na:</p>
          <ul>
            <li>Prístup k svojim osobným údajom</li>
            <li>Opravu nepresných údajov</li>
            <li>Vymazanie údajov</li>
            <li>Obmedzenie spracovania</li>
            <li>Prenosnosť údajov</li>
            <li>Námietku proti spracovaniu</li>
          </ul>

          <h2>6. Kontakt</h2>
          <p>
            V prípade otázok týkajúcich sa ochrany osobných údajov nás kontaktujte na adrese 
            <a href="mailto:gdpr@salonelegance.sk">gdpr@salonelegance.sk</a> alebo telefonicky na 
            <a href="tel:+421901234567">+421 901 234 567</a>.
          </p>

          <p class="text-sm text-gray-600 mt-8">
            Posledná aktualizácia: {{ currentDate }}
          </p>
        </div>
      </div>
    </section>

    <Footer />
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

useHead({
  title: 'Ochrana osobných údajov - Salon Elegance',
  meta: [
    { name: 'description', content: 'Informácie o ochrane osobných údajov v Salon Elegance' }
  ]
})

const currentDate = computed(() => {
  return new Date().toLocaleDateString('sk-SK', { year: 'numeric', month: 'long', day: 'numeric' })
})
</script>

<style scoped>
.prose h2 {
  @apply font-serif text-2xl font-bold text-secondary-900 mt-8 mb-4;
}

.prose p {
  @apply text-secondary-700 mb-4 leading-relaxed;
}

.prose ul {
  @apply list-disc list-inside space-y-2 text-secondary-700 mb-4;
}

.prose a {
  @apply text-primary-600 hover:text-primary-700 transition-colors;
}
</style>

