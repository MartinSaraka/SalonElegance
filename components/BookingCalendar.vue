<template>
  <div class="space-y-6">
    <!-- Calendar Header -->
    <div class="flex items-center justify-between mb-6">
      <button 
        @click="previousMonth" 
        class="p-2 rounded-lg hover:bg-primary-100 transition-colors"
        :disabled="isCurrentMonth"
      >
        <Icon name="mdi:chevron-left" class="text-2xl text-secondary-700" />
      </button>
      
      <h3 class="font-serif text-2xl font-bold text-secondary-900">
        {{ currentMonthName }} {{ currentYear }}
      </h3>
      
      <button 
        @click="nextMonth" 
        class="p-2 rounded-lg hover:bg-primary-100 transition-colors"
      >
        <Icon name="mdi:chevron-right" class="text-2xl text-secondary-700" />
      </button>
    </div>

    <!-- Calendar Grid -->
    <div class="bg-white rounded-xl shadow-lg p-6">
      <!-- Days of Week -->
      <div class="grid grid-cols-7 gap-2 mb-4">
        <div 
          v-for="day in daysOfWeek" 
          :key="day"
          class="text-center text-sm font-semibold text-secondary-600 py-2"
        >
          {{ day }}
        </div>
      </div>

      <!-- Calendar Days -->
      <div class="grid grid-cols-7 gap-2">
        <!-- Empty cells for days before month starts -->
        <div 
          v-for="blank in blanksAtStart" 
          :key="`blank-${blank}`"
          class="aspect-square"
        ></div>

        <!-- Actual days -->
        <button
          v-for="day in daysInMonth"
          :key="day"
          @click="selectDay(day)"
          :disabled="!isDayAvailable(day)"
          class="aspect-square rounded-lg text-center transition-all duration-200 relative group"
          :class="getDayClasses(day)"
        >
          <span class="relative z-10">{{ day }}</span>
          
          <!-- Available indicator -->
          <div 
            v-if="isDayAvailable(day) && !isSelectedDay(day)" 
            class="absolute bottom-1 left-1/2 transform -translate-x-1/2 w-1 h-1 bg-primary-500 rounded-full opacity-0 group-hover:opacity-100 transition-opacity"
          ></div>
          
          <!-- Tooltip for unavailable days -->
          <div 
            v-if="!isDayAvailable(day) && !isPastDay(day)"
            class="absolute bottom-full left-1/2 transform -translate-x-1/2 mb-2 px-2 py-1 bg-secondary-900 text-white text-xs rounded opacity-0 group-hover:opacity-100 transition-opacity whitespace-nowrap pointer-events-none"
          >
            Obsadené
          </div>
        </button>
      </div>
    </div>

    <!-- Selected Date Info -->
    <Transition name="slide-fade">
      <div v-if="selectedDate" ref="timeSlotsSection" class="bg-gradient-to-r from-primary-50 to-primary-100 rounded-xl p-6 border-2 border-primary-200 mt-6">
        <div class="flex items-center justify-between mb-4">
          <div>
            <p class="text-sm text-primary-700 font-semibold mb-1">Vybraný dátum</p>
            <p class="text-2xl font-bold text-secondary-900">
              {{ formatSelectedDate }}
            </p>
          </div>
          <div class="w-12 h-12 rounded-full bg-primary-500 flex items-center justify-center animate-pulse">
            <Icon name="mdi:calendar-check" class="text-2xl text-white" />
          </div>
        </div>

        <!-- Available Time Slots -->
        <div class="relative">
          <p class="text-sm font-semibold text-secondary-700 mb-4 flex items-center animate-pulse">
            <Icon name="mdi:clock-time-four" class="mr-2 text-primary-600 text-lg" />
            <span class="text-base">Vyberte si čas ({{ availableTimesForSelectedDay.length }} voľných):</span>
          </p>
          
          <div class="grid grid-cols-3 sm:grid-cols-4 md:grid-cols-6 gap-2 mb-4">
            <button
              v-for="time in availableTimesForSelectedDay"
              :key="time"
              @click="selectTime(time)"
              class="py-3 px-4 rounded-lg font-semibold text-sm transition-all duration-200"
              :class="selectedTime === time 
                ? 'bg-primary-600 text-white shadow-lg scale-105' 
                : 'bg-white text-secondary-700 hover:bg-primary-500 hover:text-white hover:scale-105 shadow'"
            >
              {{ time }}
            </button>
          </div>

          <p v-if="availableTimesForSelectedDay.length === 0" class="text-secondary-600 text-center py-4">
            Na tento deň nie sú dostupné žiadne voľné termíny.
          </p>
        </div>

        <!-- Selected Time Confirmation -->
        <Transition name="fade">
          <div v-if="selectedTime" class="mt-4 p-4 bg-white rounded-lg border-2 border-primary-300 animate-scale-in">
            <div class="flex items-center justify-between">
              <div class="flex items-center space-x-3">
                <Icon name="mdi:clock-check" class="text-2xl text-primary-600" />
                <div>
                  <p class="text-sm text-secondary-600">Vybraný čas</p>
                  <p class="text-lg font-bold text-secondary-900">{{ selectedTime }}</p>
                </div>
              </div>
              <button 
                @click="clearTimeSelection"
                class="text-secondary-500 hover:text-secondary-700 transition-colors"
              >
                <Icon name="mdi:close-circle" class="text-xl" />
              </button>
            </div>
            <div class="mt-3 p-3 bg-green-50 rounded-lg border border-green-200">
              <p class="text-sm text-green-800 flex items-center font-semibold">
                <Icon name="mdi:check-circle" class="text-green-600 mr-2 text-lg" />
                Výborně! Pokračujte nižšie na krok 3
                <Icon name="mdi:arrow-down" class="ml-2 animate-bounce" />
              </p>
            </div>
          </div>
        </Transition>
      </div>
    </Transition>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, nextTick } from 'vue'

const emit = defineEmits<{
  'update:date': [date: string]
  'update:time': [time: string]
}>()

const timeSlotsSection = ref<HTMLElement | null>(null)

// Current calendar state
const today = new Date()
const currentMonth = ref(today.getMonth())
const currentYear = ref(today.getFullYear())
const selectedDate = ref<Date | null>(null)
const selectedTime = ref<string>('')

const daysOfWeek = ['Po', 'Ut', 'St', 'Št', 'Pi', 'So', 'Ne']

// Simulated booking data (v reálnej aplikácii by to prišlo z API)
const bookedSlots = ref<Record<string, string[]>>({
  // Formát: 'YYYY-MM-DD': ['09:00', '10:00', ...]
  '2025-10-20': ['09:00', '10:00', '14:00'],
  '2025-10-21': ['09:30', '11:00', '15:00'],
  '2025-10-25': ['10:00', '11:00', '12:00', '13:00', '14:00', '15:00', '16:00']
})

// All possible time slots
const allTimeSlots = [
  '09:00', '09:30', '10:00', '10:30', '11:00', '11:30',
  '12:00', '12:30', '13:00', '13:30', '14:00', '14:30',
  '15:00', '15:30', '16:00', '16:30', '17:00', '17:30'
]

// Closed days (0 = Sunday, 6 = Saturday)
const closedDays = [0] // Nedeľa zatvorené

const currentMonthName = computed(() => {
  const months = [
    'Január', 'Február', 'Marec', 'Apríl', 'Máj', 'Jún',
    'Júl', 'August', 'September', 'Október', 'November', 'December'
  ]
  return months[currentMonth.value]
})

const daysInMonth = computed(() => {
  return new Date(currentYear.value, currentMonth.value + 1, 0).getDate()
})

const blanksAtStart = computed(() => {
  const firstDay = new Date(currentYear.value, currentMonth.value, 1).getDay()
  // Convert Sunday (0) to 7, then subtract 1 to make Monday = 0
  return firstDay === 0 ? 6 : firstDay - 1
})

const isCurrentMonth = computed(() => {
  return currentMonth.value === today.getMonth() && currentYear.value === today.getFullYear()
})

const formatSelectedDate = computed(() => {
  if (!selectedDate.value) return ''
  const days = ['Nedeľa', 'Pondelok', 'Utorok', 'Streda', 'Štvrtok', 'Piatok', 'Sobota']
  const months = [
    'januára', 'februára', 'marca', 'apríla', 'mája', 'júna',
    'júla', 'augusta', 'septembra', 'októbra', 'novembra', 'decembra'
  ]
  
  const dayName = days[selectedDate.value.getDay()]
  const day = selectedDate.value.getDate()
  const month = months[selectedDate.value.getMonth()]
  
  return `${dayName}, ${day}. ${month} ${selectedDate.value.getFullYear()}`
})

const availableTimesForSelectedDay = computed(() => {
  if (!selectedDate.value) return []
  
  const dateKey = formatDateKey(selectedDate.value)
  const bookedTimes = bookedSlots.value[dateKey] || []
  
  // Filter out booked times
  return allTimeSlots.filter(time => !bookedTimes.includes(time))
})

function formatDateKey(date: Date): string {
  const year = date.getFullYear()
  const month = String(date.getMonth() + 1).padStart(2, '0')
  const day = String(date.getDate()).padStart(2, '0')
  return `${year}-${month}-${day}`
}

function isPastDay(day: number): boolean {
  const date = new Date(currentYear.value, currentMonth.value, day)
  const todayStart = new Date(today.getFullYear(), today.getMonth(), today.getDate())
  return date < todayStart
}

function isClosedDay(day: number): boolean {
  const date = new Date(currentYear.value, currentMonth.value, day)
  return closedDays.includes(date.getDay())
}

function isDayFullyBooked(day: number): boolean {
  const date = new Date(currentYear.value, currentMonth.value, day)
  const dateKey = formatDateKey(date)
  const bookedTimes = bookedSlots.value[dateKey] || []
  return bookedTimes.length >= allTimeSlots.length
}

function isDayAvailable(day: number): boolean {
  return !isPastDay(day) && !isClosedDay(day) && !isDayFullyBooked(day)
}

function isSelectedDay(day: number): boolean {
  if (!selectedDate.value) return false
  return selectedDate.value.getDate() === day &&
         selectedDate.value.getMonth() === currentMonth.value &&
         selectedDate.value.getFullYear() === currentYear.value
}

function getDayClasses(day: number): string {
  if (isSelectedDay(day)) {
    return 'bg-primary-600 text-white shadow-lg scale-105 font-bold'
  }
  if (isPastDay(day)) {
    return 'text-secondary-300 cursor-not-allowed'
  }
  if (isClosedDay(day)) {
    return 'text-secondary-300 cursor-not-allowed line-through'
  }
  if (isDayFullyBooked(day)) {
    return 'text-secondary-400 cursor-not-allowed opacity-50'
  }
  return 'bg-secondary-50 hover:bg-primary-100 text-secondary-900 font-semibold hover:scale-110 cursor-pointer'
}

function selectDay(day: number) {
  if (!isDayAvailable(day)) return
  
  const newDate = new Date(currentYear.value, currentMonth.value, day)
  selectedDate.value = newDate
  selectedTime.value = '' // Reset time selection
  
  // Emit date to parent
  emit('update:date', formatDateKey(newDate))
  emit('update:time', '')
  
  // Scroll to time slots section after selecting a day - with small delay for smooth animation
  nextTick(() => {
    setTimeout(() => {
      if (timeSlotsSection.value) {
        const yOffset = -100; // offset from top of viewport
        const element = timeSlotsSection.value
        const y = element.getBoundingClientRect().top + window.pageYOffset + yOffset
        
        window.scrollTo({ 
          top: y, 
          behavior: 'smooth' 
        })
      }
    }, 100)
  })
}

function selectTime(time: string) {
  selectedTime.value = time
  emit('update:time', time)
}

function clearTimeSelection() {
  selectedTime.value = ''
  emit('update:time', '')
}

function previousMonth() {
  if (currentMonth.value === 0) {
    currentMonth.value = 11
    currentYear.value--
  } else {
    currentMonth.value--
  }
  // Clear selection when changing months
  selectedDate.value = null
  selectedTime.value = ''
  emit('update:date', '')
  emit('update:time', '')
}

function nextMonth() {
  if (currentMonth.value === 11) {
    currentMonth.value = 0
    currentYear.value++
  } else {
    currentMonth.value++
  }
  // Clear selection when changing months
  selectedDate.value = null
  selectedTime.value = ''
  emit('update:date', '')
  emit('update:time', '')
}
</script>

<style scoped>
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.2s ease-in;
}

.slide-fade-enter-from {
  transform: translateY(-10px);
  opacity: 0;
}

.slide-fade-leave-to {
  transform: translateY(-10px);
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

