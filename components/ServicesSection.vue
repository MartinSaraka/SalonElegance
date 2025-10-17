<template>
  <section id="sluzby" class="py-20 md:py-32 bg-gradient-to-b from-white to-secondary-50">
    <div class="container mx-auto px-4">
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-16 animate-slide-up">
        <p class="section-subtitle">Naše služby</p>
        <h2 class="section-title">Kompletná starostlivosť o vašu krásu</h2>
        <p class="text-lg text-secondary-600 mt-4">
          Ponúkame širokú škálu profesionálnych služeb prispôsobených vašim potrebám
        </p>
      </div>

      <!-- Services Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="(service, index) in services" :key="index" 
          class="card group hover:scale-105 transition-transform duration-300 animate-scale-in"
          :style="`animation-delay: ${index * 0.1}s`">
          <div class="relative h-64 overflow-hidden">
            <img :src="service.image" :alt="service.title" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500" />
            <div class="gradient-overlay"></div>
            <div class="absolute bottom-4 left-4 text-white">
              <Icon :name="service.icon" class="text-4xl mb-2" />
            </div>
          </div>
          <div class="p-6">
            <h3 class="font-serif text-2xl font-bold text-secondary-900 mb-2">{{ service.title }}</h3>
            <p class="text-secondary-600 mb-4">{{ service.description }}</p>
            <div class="flex justify-between items-center">
              <span class="text-primary-600 font-bold text-xl">od {{ service.price }}€</span>
              <span class="text-secondary-500 text-sm">{{ service.duration }}</span>
            </div>
          </div>
        </div>
      </div>

      <!-- CTA -->
      <div class="text-center mt-16">
        <NuxtLink to="/rezervacia" class="btn-primary text-lg">
          Rezervovať službu
          <Icon name="mdi:calendar-check" class="inline ml-2" />
        </NuxtLink>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const services = [
  {
    title: 'Dámske strihanie',
    description: 'Moderné strihy prispôsobené vášmu typu vlasov a tvaru tváre',
    price: '25',
    duration: '60 min',
    icon: 'mdi:content-cut',
    image: 'https://images.unsplash.com/photo-1562322140-8baeececf3df?q=80&w=2069&auto=format&fit=crop'
  },
  {
    title: 'Pánske strihanie',
    description: 'Klasické aj moderné pánske strihy a úprava brady',
    price: '18',
    duration: '45 min',
    icon: 'mdi:face-man',
    image: 'https://images.unsplash.com/photo-1503951914875-452162b0f3f1?q=80&w=2070&auto=format&fit=crop'
  },
  {
    title: 'Farbenie',
    description: 'Profesionálne farbenie s prémiovou kozmetikou',
    price: '45',
    duration: '120 min',
    icon: 'mdi:palette',
    image: 'https://images.unsplash.com/photo-1522338140262-f46f5913618a?q=80&w=2146&auto=format&fit=crop'
  },
  {
    title: 'Melírovanie',
    description: 'Jemné zvýraznenie vlasov pre prirodzený vzhľad',
    price: '55',
    duration: '150 min',
    icon: 'mdi:brush',
    image: 'https://images.unsplash.com/photo-1519699047748-de8e457a634e?q=80&w=2080&auto=format&fit=crop'
  },
  {
    title: 'Keratínová kúra',
    description: 'Regenerácia a vyhladzovanie vlasov s dlhodobým efektom',
    price: '80',
    duration: '180 min',
    icon: 'mdi:sparkles',
    image: 'https://images.unsplash.com/photo-1580618672591-eb180b1a973f?q=80&w=2069&auto=format&fit=crop'
  },
  {
    title: 'Svadobné účesy',
    description: 'Dokonalý účes pre váš veľký deň vrátane skúšky',
    price: '120',
    duration: '240 min',
    icon: 'mdi:crown',
    image: 'https://images.unsplash.com/photo-1487412947147-5cebf100ffc2?q=80&w=2071&auto=format&fit=crop'
  }
]
</script>

