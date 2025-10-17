<template>
  <nav class="fixed top-0 left-0 right-0 z-50 transition-all duration-300" :class="scrolled ? 'bg-white shadow-lg' : 'bg-transparent'">
    <div class="container mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-20">
        <!-- Logo -->
        <NuxtLink to="/" class="flex items-center space-x-2 group">
          <Icon name="mdi:scissors-cutting" class="text-3xl text-primary-600 group-hover:rotate-12 transition-transform duration-300" />
          <span class="font-serif text-2xl font-bold" :class="scrolled ? 'text-secondary-900' : 'text-white'">
            Salon Elegance
          </span>
        </NuxtLink>

        <!-- Desktop Menu -->
        <div class="hidden md:flex items-center space-x-8">
          <NuxtLink v-for="item in menuItems" :key="item.to" :to="item.to" 
            class="font-medium transition-colors duration-200 hover:text-primary-600"
            :class="scrolled ? 'text-secondary-700' : 'text-white'">
            {{ item.label }}
          </NuxtLink>
          <NuxtLink to="/rezervacia" class="btn-primary">
            Rezervovať
          </NuxtLink>
        </div>

        <!-- Mobile Menu Button -->
        <button @click="mobileMenuOpen = !mobileMenuOpen" class="md:hidden p-2 rounded-lg" :class="scrolled ? 'text-secondary-900' : 'text-white'">
          <Icon :name="mobileMenuOpen ? 'mdi:close' : 'mdi:menu'" class="text-3xl" />
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <Transition name="slide-fade">
      <div v-if="mobileMenuOpen" class="md:hidden bg-white border-t shadow-lg">
        <div class="container mx-auto px-4 py-6 space-y-4">
          <NuxtLink v-for="item in menuItems" :key="item.to" :to="item.to" 
            @click="mobileMenuOpen = false"
            class="block text-lg font-medium text-secondary-700 hover:text-primary-600 transition-colors">
            {{ item.label }}
          </NuxtLink>
          <NuxtLink to="/rezervacia" @click="mobileMenuOpen = false" class="block btn-primary text-center">
            Rezervovať
          </NuxtLink>
        </div>
      </div>
    </Transition>
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const mobileMenuOpen = ref(false)

const menuItems = [
  { label: 'Domov', to: '/' },
  { label: 'Služby', to: '/#sluzby' },
  { label: 'Galéria', to: '/#galeria' },
  { label: 'Kontakt', to: '/#kontakt' }
]

const handleScroll = () => {
  scrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.3s ease;
}

.slide-fade-enter-from {
  transform: translateY(-10px);
  opacity: 0;
}

.slide-fade-leave-to {
  transform: translateY(-10px);
  opacity: 0;
}
</style>

