<template>
  <section id="galeria" class="py-20 md:py-32 bg-white">
    <div class="container mx-auto px-4">
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-16">
        <p class="section-subtitle">Galéria</p>
        <h2 class="section-title">Naša práca hovorí za nás</h2>
        <p class="text-lg text-secondary-600 mt-4">
          Pozrite si ukázky našich najlepších prác a nechajte sa inšpirovať
        </p>
      </div>

      <!-- Gallery Grid -->
      <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
        <div v-for="(image, index) in galleryImages" :key="index"
          class="relative overflow-hidden rounded-xl group cursor-pointer aspect-square"
          :class="index % 7 === 0 ? 'md:col-span-2 md:row-span-2' : ''"
          @click="openLightbox(index)">
          <img :src="image.url" :alt="image.alt" 
            class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500" />
          <div class="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
            <p class="text-white font-semibold">{{ image.alt }}</p>
          </div>
          <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300">
            <Icon name="mdi:magnify-plus" class="text-white text-5xl" />
          </div>
        </div>
      </div>

      <!-- Lightbox -->
      <Transition name="fade">
        <div v-if="lightboxOpen" 
          class="fixed inset-0 z-50 bg-black/95 flex items-center justify-center p-4"
          @click="closeLightbox">
          <button @click="closeLightbox" class="absolute top-4 right-4 text-white text-4xl hover:text-primary-400 transition-colors">
            <Icon name="mdi:close" />
          </button>
          <button @click.stop="previousImage" class="absolute left-4 text-white text-4xl hover:text-primary-400 transition-colors">
            <Icon name="mdi:chevron-left" />
          </button>
          <button @click.stop="nextImage" class="absolute right-4 text-white text-4xl hover:text-primary-400 transition-colors">
            <Icon name="mdi:chevron-right" />
          </button>
          <img :src="galleryImages[currentImageIndex].url" 
            :alt="galleryImages[currentImageIndex].alt"
            class="max-h-[90vh] max-w-[90vw] object-contain"
            @click.stop />
        </div>
      </Transition>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const lightboxOpen = ref(false)
const currentImageIndex = ref(0)

const galleryImages = [
  { url: 'https://images.unsplash.com/photo-1560066984-138dadb4c035?q=80&w=2074&auto=format&fit=crop', alt: 'Moderný dámsky strih' },
  { url: 'https://images.unsplash.com/photo-1562322140-8baeececf3df?q=80&w=2069&auto=format&fit=crop', alt: 'Elegantný účes' },
  { url: 'https://images.unsplash.com/photo-1522338140262-f46f5913618a?q=80&w=2146&auto=format&fit=crop', alt: 'Profesionálne farbenie' },
  { url: 'https://images.unsplash.com/photo-1503951914875-452162b0f3f1?q=80&w=2070&auto=format&fit=crop', alt: 'Pánsky strih' },
  { url: 'https://images.unsplash.com/photo-1519699047748-de8e457a634e?q=80&w=2080&auto=format&fit=crop', alt: 'Melírovanie' },
  { url: 'https://images.unsplash.com/photo-1580618672591-eb180b1a973f?q=80&w=2069&auto=format&fit=crop', alt: 'Keratínová kúra' },
  { url: 'https://images.unsplash.com/photo-1487412947147-5cebf100ffc2?q=80&w=2071&auto=format&fit=crop', alt: 'Svadobný účes' },
  { url: 'https://images.unsplash.com/photo-1492106087820-71f1a00d2b11?q=80&w=2074&auto=format&fit=crop', alt: 'Styling' },
  { url: 'https://images.unsplash.com/photo-1521590832167-7bcbfaa6381f?q=80&w=2070&auto=format&fit=crop', alt: 'Moderný look' },
  { url: 'https://images.unsplash.com/photo-1595475884562-073c30d45670?q=80&w=2070&auto=format&fit=crop', alt: 'Kreatívne farbenie' },
  { url: 'https://images.unsplash.com/photo-1605497788044-5a32c7078486?q=80&w=2070&auto=format&fit=crop', alt: 'Luxusný účes' },
  { url: 'https://images.unsplash.com/photo-1516975080664-ed2fc6a32937?q=80&w=2070&auto=format&fit=crop', alt: 'Vlnité vlasy' }
]

const openLightbox = (index: number) => {
  currentImageIndex.value = index
  lightboxOpen.value = true
  document.body.style.overflow = 'hidden'
}

const closeLightbox = () => {
  lightboxOpen.value = false
  document.body.style.overflow = ''
}

const nextImage = () => {
  currentImageIndex.value = (currentImageIndex.value + 1) % galleryImages.length
}

const previousImage = () => {
  currentImageIndex.value = (currentImageIndex.value - 1 + galleryImages.length) % galleryImages.length
}
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

