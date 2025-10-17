<template>
  <Transition name="slide-fade">
    <div v-if="showSummary" class="sticky top-24 bg-white rounded-xl shadow-xl p-6 border-2 border-primary-200">
      <h4 class="font-serif text-xl font-bold text-secondary-900 mb-4 flex items-center">
        <Icon name="mdi:clipboard-text" class="text-primary-600 mr-2" />
        Zhrnutie rezervácie
      </h4>
      
      <div class="space-y-3">
        <!-- Service -->
        <div v-if="service" class="flex items-start">
          <Icon name="mdi:scissors-cutting" class="text-primary-600 mt-1 mr-3 flex-shrink-0" />
          <div>
            <p class="text-xs text-secondary-600">Služba</p>
            <p class="font-semibold text-secondary-900">{{ service }}</p>
          </div>
        </div>
        
        <!-- Date -->
        <div v-if="date" class="flex items-start">
          <Icon name="mdi:calendar" class="text-primary-600 mt-1 mr-3 flex-shrink-0" />
          <div>
            <p class="text-xs text-secondary-600">Dátum</p>
            <p class="font-semibold text-secondary-900">{{ formattedDate }}</p>
          </div>
        </div>
        
        <!-- Time -->
        <div v-if="time" class="flex items-start">
          <Icon name="mdi:clock" class="text-primary-600 mt-1 mr-3 flex-shrink-0" />
          <div>
            <p class="text-xs text-secondary-600">Čas</p>
            <p class="font-semibold text-secondary-900">{{ time }}</p>
          </div>
        </div>
      </div>
      
      <div v-if="!service || !date || !time" class="mt-4 pt-4 border-t border-secondary-200">
        <p class="text-xs text-secondary-600 flex items-center">
          <Icon name="mdi:information-outline" class="mr-1 text-primary-600" />
          Postupne vyplňte jednotlivé kroky
        </p>
      </div>
      
      <div v-else class="mt-4 pt-4 border-t border-secondary-200">
        <div class="flex items-center text-green-600 text-sm">
          <Icon name="mdi:check-circle" class="mr-2" />
          <span class="font-semibold">Termín vybraný!</span>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  service?: string
  date?: string
  time?: string
}>()

const showSummary = computed(() => {
  return props.service || props.date || props.time
})

const formattedDate = computed(() => {
  if (!props.date) return ''
  
  const [year, month, day] = props.date.split('-')
  const date = new Date(parseInt(year), parseInt(month) - 1, parseInt(day))
  
  const days = ['Nedeľa', 'Pondelok', 'Utorok', 'Streda', 'Štvrtok', 'Piatok', 'Sobota']
  const months = [
    'januára', 'februára', 'marca', 'apríla', 'mája', 'júna',
    'júla', 'augusta', 'septembra', 'októbra', 'novembra', 'decembra'
  ]
  
  return `${days[date.getDay()]}, ${date.getDate()}. ${months[date.getMonth()]} ${date.getFullYear()}`
})
</script>

<style scoped>
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.2s ease-in;
}

.slide-fade-enter-from {
  transform: translateX(20px);
  opacity: 0;
}

.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>

