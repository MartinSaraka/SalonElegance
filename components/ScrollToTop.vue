<template>
  <Transition name="fade">
    <button
      v-if="showButton"
      @click="scrollToTop"
      class="fixed bottom-8 right-8 z-40 w-12 h-12 rounded-full bg-primary-600 hover:bg-primary-700 text-white shadow-lg hover:shadow-xl transition-all duration-300 flex items-center justify-center group"
      aria-label="Scroll to top"
    >
      <Icon name="mdi:arrow-up" class="text-2xl group-hover:-translate-y-1 transition-transform" />
    </button>
  </Transition>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const showButton = ref(false)

const handleScroll = () => {
  showButton.value = window.scrollY > 300
}

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  })
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

