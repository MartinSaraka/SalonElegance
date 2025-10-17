<template>
  <section class="relative h-screen flex items-center justify-center overflow-hidden">
    <!-- Background Image with Overlay -->
    <div class="absolute inset-0 z-0">
      <div class="absolute inset-0 bg-gradient-to-br from-primary-900/40 via-secondary-900/50 to-primary-800/40 z-10"></div>
      <img 
        src="https://images.unsplash.com/photo-1560066984-138dadb4c035?q=80&w=2074&auto=format&fit=crop"
        alt="Salon Interior"
        class="w-full h-full object-cover"
      />
    </div>

    <!-- Animated Background Elements -->
    <div class="absolute inset-0 z-10 overflow-hidden">
      <div class="absolute top-20 left-10 w-72 h-72 bg-primary-500/10 rounded-full blur-3xl animate-pulse"></div>
      <div class="absolute bottom-20 right-10 w-96 h-96 bg-primary-400/10 rounded-full blur-3xl animate-pulse" style="animation-delay: 1s"></div>
    </div>

    <!-- Content -->
    <div class="relative z-20 container mx-auto px-4 text-center">
      <div class="max-w-4xl mx-auto space-y-8 animate-fade-in">
        <div class="space-y-4">
          <p class="text-primary-300 font-semibold text-lg md:text-xl uppercase tracking-widest animate-slide-down">
            Váš štýl, naša vášeň
          </p>
          <h1 class="font-serif text-5xl md:text-7xl lg:text-8xl font-bold text-white leading-tight animate-slide-up">
            Kde krása<br />stretáva umenie
          </h1>
          <p class="text-xl md:text-2xl text-gray-200 max-w-2xl mx-auto animate-slide-up" style="animation-delay: 0.2s">
            Profesionálne kaderníctvo a kozmetické služby pre vašu dokonalú transformáciu
          </p>
        </div>

        <div class="flex flex-col sm:flex-row gap-4 justify-center items-center animate-scale-in" style="animation-delay: 0.4s">
          <NuxtLink to="/rezervacia" class="btn-primary text-lg px-12 py-4 group">
            Rezervovať termín
            <Icon name="mdi:arrow-right" class="inline ml-2 group-hover:translate-x-2 transition-transform" />
          </NuxtLink>
          <a href="#sluzby" class="btn-secondary text-lg px-12 py-4">
            Naše služby
          </a>
        </div>

        <!-- Features -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-16 animate-fade-in max-w-2xl md:max-w-4xl mx-auto" style="animation-delay: 0.6s">
          <div class="flex items-center md:justify-center space-x-4 text-white bg-white/10 backdrop-blur-sm rounded-xl p-4 md:bg-transparent md:backdrop-blur-none">
            <div class="flex-shrink-0">
              <Icon name="mdi:clock-outline" class="text-4xl md:text-3xl text-primary-400" />
            </div>
            <div class="text-left">
              <p class="font-bold text-xl md:text-lg leading-tight">15+ rokov</p>
              <p class="text-sm text-gray-300">Skúseností</p>
            </div>
          </div>
          <div class="flex items-center md:justify-center space-x-4 text-white bg-white/10 backdrop-blur-sm rounded-xl p-4 md:bg-transparent md:backdrop-blur-none">
            <div class="flex-shrink-0">
              <Icon name="mdi:account-group" class="text-4xl md:text-3xl text-primary-400" />
            </div>
            <div class="text-left">
              <p class="font-bold text-xl md:text-lg leading-tight">5000+</p>
              <p class="text-sm text-gray-300">Spokojných klientov</p>
            </div>
          </div>
          <div class="flex items-center md:justify-center space-x-4 text-white bg-white/10 backdrop-blur-sm rounded-xl p-4 md:bg-transparent md:backdrop-blur-none">
            <div class="flex-shrink-0">
              <Icon name="mdi:star" class="text-4xl md:text-3xl text-primary-400" />
            </div>
            <div class="text-left">
              <p class="font-bold text-xl md:text-lg leading-tight">4.9/5</p>
              <p class="text-sm text-gray-300">Hodnotenie</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Scroll Indicator -->
    <div class="absolute bottom-10 left-1/2 transform -translate-x-1/2 z-20 animate-bounce">
      <a href="#sluzby" class="text-white">
        <Icon name="mdi:chevron-down" class="text-4xl" />
      </a>
    </div>
  </section>
</template>

<script setup lang="ts">
</script>

