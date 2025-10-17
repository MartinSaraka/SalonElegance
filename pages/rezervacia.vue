<template>
  <div>
    <Navigation />
    
    <!-- Page Header -->
    <section class="pt-32 pb-16 bg-gradient-to-br from-primary-300 to-primary-800 text-white">
      <div class="container mx-auto px-4 text-center">
        <h1 class="font-serif text-5xl md:text-6xl font-bold mb-4">Rezervácia termínu</h1>
        <p class="text-xl text-primary-100 max-w-2xl mx-auto">
          Naplánujte si vašu návštevu v salóne pohodlne online
        </p>
      </div>
    </section>

    <BookingForm />
    
    <!-- Benefits -->
    <section class="py-20 bg-white">
      <div class="container mx-auto px-4">
        <h2 class="text-center font-serif text-3xl md:text-4xl font-bold text-secondary-900 mb-12">
          Prečo rezervovať online?
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-5xl mx-auto">
          <div class="text-center">
            <div class="w-16 h-16 rounded-full bg-primary-100 flex items-center justify-center mx-auto mb-4">
              <Icon name="mdi:clock-fast" class="text-3xl text-primary-600" />
            </div>
            <h3 class="font-semibold text-xl mb-2">Rýchle a jednoduché</h3>
            <p class="text-secondary-600">Rezervácia trvá len pár minút</p>
          </div>
          <div class="text-center">
            <div class="w-16 h-16 rounded-full bg-primary-100 flex items-center justify-center mx-auto mb-4">
              <Icon name="mdi:calendar-check" class="text-3xl text-primary-600" />
            </div>
            <h3 class="font-semibold text-xl mb-2">Dostupné 24/7</h3>
            <p class="text-secondary-600">Rezervujte kedykoľvek vám to vyhovuje</p>
          </div>
          <div class="text-center">
            <div class="w-16 h-16 rounded-full bg-primary-100 flex items-center justify-center mx-auto mb-4">
              <Icon name="mdi:shield-check" class="text-3xl text-primary-600" />
            </div>
            <h3 class="font-semibold text-xl mb-2">Potvrdenie emailom</h3>
            <p class="text-secondary-600">Okamžité potvrdenie rezervácie</p>
          </div>
        </div>
      </div>
    </section>

    <Footer />
    <ScrollToTop />
  </div>
</template>

<script setup lang="ts">
useHead({
  title: 'Online rezervácia - Salon Elegance',
  meta: [
    { name: 'description', content: 'Rezervujte si termín v našom salóne online. Rýchle a jednoduché online rezervácie dostupné 24/7.' }
  ]
})
</script>

