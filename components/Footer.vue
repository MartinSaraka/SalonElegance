<template>
  <footer class="bg-secondary-900 text-white py-12">
    <div class="container mx-auto px-4">
      <div class="grid grid-cols-1 md:grid-cols-4 gap-8 mb-8">
        <!-- About -->
        <div class="md:col-span-2">
          <div class="flex items-center space-x-2 mb-4">
            <Icon name="mdi:scissors-cutting" class="text-3xl text-primary-400" />
            <span class="font-serif text-2xl font-bold">Salon Elegance</span>
          </div>
          <p class="text-gray-400 mb-4 max-w-md">
            Profesionálne kaderníctvo a kozmetické služby v srdci Bratislavy. 
            Vytvárame krásu s vášňou a precíznosťou už viac ako 15 rokov. Ide o fiktívny salon pre demonstráciu možnosti webu na mieru pre kaderníctvo/barber shop od firmy Appinara.
          </p>
          <div class="flex space-x-4">
            <a href="#" class="w-10 h-10 rounded-full bg-secondary-800 hover:bg-primary-600 flex items-center justify-center transition-colors">
              <Icon name="mdi:facebook" class="text-xl" />
            </a>
            <a href="#" class="w-10 h-10 rounded-full bg-secondary-800 hover:bg-primary-600 flex items-center justify-center transition-colors">
              <Icon name="mdi:instagram" class="text-xl" />
            </a>
            <a href="#" class="w-10 h-10 rounded-full bg-secondary-800 hover:bg-primary-600 flex items-center justify-center transition-colors">
              <Icon name="mdi:youtube" class="text-xl" />
            </a>
          </div>
        </div>

        <!-- Quick Links -->
        <div>
          <h3 class="font-semibold text-lg mb-4">Rýchle odkazy</h3>
          <ul class="space-y-2">
            <li><NuxtLink to="/" class="text-gray-400 hover:text-primary-400 transition-colors">Domov</NuxtLink></li>
            <li><NuxtLink to="/#sluzby" class="text-gray-400 hover:text-primary-400 transition-colors">Služby</NuxtLink></li>
            <li><NuxtLink to="/#galeria" class="text-gray-400 hover:text-primary-400 transition-colors">Galéria</NuxtLink></li>
            <li><NuxtLink to="/rezervacia" class="text-gray-400 hover:text-primary-400 transition-colors">Rezervácia</NuxtLink></li>
          </ul>
        </div>

        <!-- Contact -->
        <div>
          <h3 class="font-semibold text-lg mb-4">Kontakt</h3>
          <ul class="space-y-3 text-gray-400">
            <li class="flex items-start space-x-2">
              <Icon name="mdi:map-marker" class="text-primary-400 mt-1 flex-shrink-0" />
              <span>Hlavná ulica 123<br />Bratislava</span>
            </li>
            <li class="flex items-center space-x-2">
              <Icon name="mdi:phone" class="text-primary-400 flex-shrink-0" />
              <a href="tel:+421901234567" class="hover:text-primary-400 transition-colors">+421 901 234 567</a>
            </li>
            <li class="flex items-center space-x-2">
              <Icon name="mdi:email" class="text-primary-400 flex-shrink-0" />
              <a href="mailto:info@salonelegance.sk" class="hover:text-primary-400 transition-colors">info@salonelegance.sk</a>
            </li>
          </ul>
        </div>
      </div>

      <!-- Bottom Bar -->
      <div class="border-t border-secondary-800 pt-8 flex flex-col md:flex-row justify-between items-center space-y-4 md:space-y-0">
        <p class="text-gray-400 text-sm">
          © {{ currentYear }} Salon Elegance. Všetky práva vyhradené.
        </p>
        <div class="flex space-x-6 text-sm">
          <NuxtLink to="/ochrana-udajov" class="text-gray-400 hover:text-primary-400 transition-colors">
            Ochrana údajov
          </NuxtLink>
          <NuxtLink to="/obchodne-podmienky" class="text-gray-400 hover:text-primary-400 transition-colors">
            Obchodné podmienky
          </NuxtLink>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const currentYear = computed(() => new Date().getFullYear())
</script>

