<template>
  <section class="py-20 md:py-32 bg-secondary-900 text-white">
    <div class="container mx-auto px-4">
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-16">
        <p class="text-primary-400 font-semibold text-sm md:text-base uppercase tracking-wider mb-2">
          Referencie
        </p>
        <h2 class="font-serif text-4xl md:text-5xl font-bold mb-4">
          Čo hovoria naši klienti
        </h2>
        <p class="text-lg text-gray-300">
          Vaša spokojnosť je naša najväčšia odmena
        </p>
      </div>

      <!-- Testimonials Grid -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <div v-for="(testimonial, index) in testimonials" :key="index"
          class="bg-secondary-800 rounded-2xl p-8 hover:bg-secondary-700 transition-colors duration-300">
          <div class="flex items-center mb-4">
            <div class="flex text-primary-400">
              <Icon v-for="i in 5" :key="i" name="mdi:star" class="text-xl" />
            </div>
          </div>
          <p class="text-gray-300 mb-6 italic">
            "{{ testimonial.text }}"
          </p>
          <div class="flex items-center">
            <div class="w-12 h-12 rounded-full bg-primary-600 flex items-center justify-center text-white font-bold text-lg mr-4">
              {{ testimonial.name.charAt(0) }}
            </div>
            <div>
              <p class="font-semibold">{{ testimonial.name }}</p>
              <p class="text-sm text-gray-400">{{ testimonial.service }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const testimonials = [
  {
    name: 'Petra Nováková',
    service: 'Dámske strihanie',
    text: 'Úžasný prístup a profesionalita. Konečne som našla kaderníčku, ktorá chápe moje vlasy. Chodím sem už rok a stále som nadšená!'
  },
  {
    name: 'Martin Kováč',
    service: 'Pánske strihanie',
    text: 'Skvelé miesto s priateľskou atmosférou. Vždy odchádzam spokojný a strih vydrží dlho. Určite odporúčam!'
  },
  {
    name: 'Lucia Horváthová',
    service: 'Svadobný účes',
    text: 'Pre môj svadobný deň vytvorili absolútne dokonalý účes. Všetko prebehlo hladko a cítila som sa ako princezná. Ďakujem!'
  }
]
</script>

