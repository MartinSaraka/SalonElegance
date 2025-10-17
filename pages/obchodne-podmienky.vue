<template>
  <div>
    <Navigation />
    
    <!-- Page Header -->
    <section class="pt-32 pb-16 bg-gradient-to-br from-secondary-800 to-secondary-900 text-white">
      <div class="container mx-auto px-4 text-center">
        <h1 class="font-serif text-4xl md:text-5xl font-bold mb-4">Obchodné podmienky</h1>
        <p class="text-lg text-gray-300 max-w-2xl mx-auto">
          Pravidlá poskytovania služieb v našom salóne
        </p>
      </div>
    </section>

    <!-- Content -->
    <section class="py-20 bg-white">
      <div class="container mx-auto px-4 max-w-4xl">
        <div class="prose prose-lg max-w-none">
          <h2>1. Základné ustanovenia</h2>
          <p>
            Tieto obchodné podmienky upravujú vzťahy medzi prevádzkovateľom Salon Elegance s.r.o. 
            a klientmi využívajúcimi služby salónu.
          </p>

          <h2>2. Rezervácia termínu</h2>
          <ul>
            <li>Rezerváciu je možné vykonať online, telefonicky alebo osobne</li>
            <li>Rezervácia je záväzná po jej potvrdení zo strany salónu</li>
            <li>V prípade potreby zrušenia rezervácie je nutné informovať salón minimálne 24 hodín vopred</li>
            <li>Pri opakovanom nezjavení sa na rezervovaný termín si vyhradzujeme právo požadovať zálohu</li>
          </ul>

          <h2>3. Cenník a platobné podmienky</h2>
          <ul>
            <li>Aktuálny cenník služieb je dostupný v salóne a na webovej stránke</li>
            <li>Ceny zahŕňajú všetky poplatky a DPH</li>
            <li>Platba je možná v hotovosti alebo platobnou kartou</li>
            <li>Pri špeciálnych službách môže byť požadovaná záloha</li>
          </ul>

          <h2>4. Reklamácie</h2>
          <ul>
            <li>Reklamácie je možné uplatniť do 7 dní od poskytnutia služby</li>
            <li>Reklamácie vybavujeme do 14 pracovných dní</li>
            <li>Pri oprávnenej reklamácii poskytneme nápravu zadarmo</li>
          </ul>

          <h2>5. Zodpovednosť</h2>
          <p>
            Salón nenesie zodpovednosť za:
          </p>
          <ul>
            <li>Alergické reakcie na použité prípravky (odporúčame vopred informovať o alergiách)</li>
            <li>Výsledok služby, ak klient neposkytol pravdivé informácie o predchádzajúcich úpravách</li>
            <li>Cennosti zanechané v salóne</li>
          </ul>

          <h2>6. Zrušenie služby zo strany salónu</h2>
          <p>
            Vyhradzujeme si právo zrušiť službu v prípade:
          </p>
          <ul>
            <li>Nepriaznivých vonkajších podmienok (napr. prírodná katastrofa)</li>
            <li>Ochorenia stylistu</li>
            <li>Nevhodného správania klienta</li>
          </ul>

          <h2>7. Záverečné ustanovenia</h2>
          <p>
            Tieto obchodné podmienky nadobúdajú účinnosť dňom ich zverejnenia. 
            Vyhradzujeme si právo zmeny obchodných podmienok.
          </p>

          <h2>8. Kontakt pre riešenie sporov</h2>
          <p>
            V prípade sporov nás kontaktujte na: <a href="mailto:info@salonelegance.sk">info@salonelegance.sk</a>
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
  title: 'Obchodné podmienky - Salon Elegance',
  meta: [
    { name: 'description', content: 'Obchodné podmienky poskytovania služieb v Salon Elegance' }
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

