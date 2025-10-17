<template>
  <section class="py-20 md:py-32 bg-gradient-to-br from-primary-50 via-white to-secondary-50">
    <div class="container mx-auto px-4">
      <!-- Section Header -->
      <div class="text-center mb-12">
        <p class="section-subtitle">Online rezervácia</p>
        <h2 class="section-title">Rezervujte si termín</h2>
        <p class="text-lg text-secondary-600 mt-4">
          Vyplňte formulár a my vás budeme kontaktovať pre potvrdenie termínu
        </p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 max-w-7xl mx-auto">
        <!-- Booking Form - Main Content -->
        <div class="lg:col-span-2">
          <form @submit.prevent="submitBooking" class="space-y-8">
          <!-- Service Selection -->
          <div class="card p-8">
            <div class="flex items-center mb-6">
              <div class="w-12 h-12 rounded-full bg-primary-600 text-white flex items-center justify-center font-bold text-lg mr-4">
                1
              </div>
              <div>
                <h3 class="text-2xl font-serif font-bold text-secondary-900">Vyberte službu</h3>
                <p class="text-secondary-600">Čo pre vás môžeme urobiť?</p>
              </div>
            </div>
            
            <div>
              <label for="service" class="block text-sm font-semibold text-secondary-700 mb-3">
                Služba *
              </label>
              <select 
                v-model="form.service"
                id="service" 
                required
                class="w-full px-4 py-3 rounded-lg border-2 border-secondary-200 focus:border-primary-500 focus:ring-2 focus:ring-primary-200 transition-colors outline-none text-lg"
              >
                <option value="">Vyberte službu</option>
                <option v-for="service in services" :key="service" :value="service">
                  {{ service }}
                </option>
              </select>
            </div>
          </div>

          <!-- Calendar Selection -->
          <div class="card p-8" id="calendar-section">
            <div class="flex items-center mb-6">
              <div class="w-12 h-12 rounded-full bg-primary-600 text-white flex items-center justify-center font-bold text-lg mr-4">
                2
              </div>
              <div>
                <h3 class="text-2xl font-serif font-bold text-secondary-900">Vyberte termín</h3>
                <p class="text-secondary-600">
                  <span v-if="!form.date">Kliknite na dostupný deň</span>
                  <span v-else-if="!form.time" class="text-primary-600 font-semibold">
                    <Icon name="mdi:arrow-down" class="inline animate-bounce" />
                    Teraz vyberte čas nižšie
                  </span>
                  <span v-else class="text-green-600 font-semibold">
                    <Icon name="mdi:check-circle" class="inline" />
                    Termín vybraný!
                  </span>
                </p>
              </div>
            </div>
            
            <BookingCalendar 
              @update:date="form.date = $event"
              @update:time="form.time = $event"
            />
            
            <BookingLegend />
          </div>

          <!-- Personal Information -->
          <div class="card p-8" :class="!form.date || !form.time ? 'opacity-50 pointer-events-none' : ''">
            <div class="flex items-center mb-6">
              <div class="w-12 h-12 rounded-full text-white flex items-center justify-center font-bold text-lg mr-4 transition-colors"
                :class="form.date && form.time ? 'bg-primary-600' : 'bg-secondary-400'">
                3
              </div>
              <div>
                <h3 class="text-2xl font-serif font-bold text-secondary-900">Vaše údaje</h3>
                <p class="text-secondary-600">
                  <span v-if="!form.date || !form.time">
                    <Icon name="mdi:information" class="inline text-primary-600" />
                    Najprv vyberte dátum a čas
                  </span>
                  <span v-else>Aby sme vás mohli kontaktovať</span>
                </p>
              </div>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <!-- Name -->
              <div>
                <label for="name" class="block text-sm font-semibold text-secondary-700 mb-2">
                  Meno a priezvisko *
                </label>
                <input 
                  v-model="form.name"
                  type="text" 
                  id="name" 
                  required
                  class="w-full px-4 py-3 rounded-lg border-2 border-secondary-200 focus:border-primary-500 focus:ring-2 focus:ring-primary-200 transition-colors outline-none"
                  placeholder="Vaše meno"
                />
              </div>

              <!-- Phone -->
              <div>
                <label for="phone" class="block text-sm font-semibold text-secondary-700 mb-2">
                  Telefón *
                </label>
                <input 
                  v-model="form.phone"
                  type="tel" 
                  id="phone" 
                  required
                  class="w-full px-4 py-3 rounded-lg border-2 border-secondary-200 focus:border-primary-500 focus:ring-2 focus:ring-primary-200 transition-colors outline-none"
                  placeholder="+421"
                />
              </div>

              <!-- Email -->
              <div class="md:col-span-2">
                <label for="email" class="block text-sm font-semibold text-secondary-700 mb-2">
                  Email *
                </label>
                <input 
                  v-model="form.email"
                  type="email" 
                  id="email" 
                  required
                  class="w-full px-4 py-3 rounded-lg border-2 border-secondary-200 focus:border-primary-500 focus:ring-2 focus:ring-primary-200 transition-colors outline-none"
                  placeholder="vas@email.sk"
                />
              </div>

              <!-- Message -->
              <div class="md:col-span-2">
                <label for="message" class="block text-sm font-semibold text-secondary-700 mb-2">
                  Poznámka (voliteľné)
                </label>
                <textarea 
                  v-model="form.message"
                  id="message" 
                  rows="4"
                  class="w-full px-4 py-3 rounded-lg border-2 border-secondary-200 focus:border-primary-500 focus:ring-2 focus:ring-primary-200 transition-colors outline-none resize-none"
                  placeholder="Máte nejaké špeciálne požiadavky alebo otázky?"
                ></textarea>
              </div>
            </div>
          </div>

          <!-- Submit Button -->
          <div class="text-center">
            <button 
              type="submit" 
              :disabled="isSubmitting || !isFormValid"
              class="btn-primary text-lg px-12 py-4 disabled:opacity-50 disabled:cursor-not-allowed"
            >
              <span v-if="!isSubmitting">
                Potvrdiť rezerváciu
                <Icon name="mdi:check-circle" class="inline ml-2" />
              </span>
              <span v-else>
                <Icon name="mdi:loading" class="inline animate-spin mr-2" />
                Odosiela sa...
              </span>
            </button>
            
            <p v-if="!isFormValid" class="text-sm text-secondary-500 mt-3">
              Vyplňte všetky povinné polia
            </p>
          </div>

          <!-- Success/Error Message -->
          <Transition name="fade">
            <div v-if="submitMessage" 
              class="mt-6 p-4 rounded-lg"
              :class="submitSuccess ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'">
              <div class="flex items-center">
                <Icon :name="submitSuccess ? 'mdi:check-circle' : 'mdi:alert-circle'" class="text-2xl mr-2" />
                <p>{{ submitMessage }}</p>
              </div>
            </div>
          </Transition>
          </form>

          <!-- Contact Info -->
          <div class="mt-8 text-center card p-6">
            <p class="text-secondary-600 mb-4 font-semibold">Alebo nás kontaktujte priamo:</p>
            <div class="flex flex-col sm:flex-row justify-center items-center gap-6">
              <a href="tel:+421901234567" class="flex items-center gap-2 text-primary-600 hover:text-primary-700 font-semibold transition-colors">
                <Icon name="mdi:phone" class="text-xl" />
                +421 901 234 567
              </a>
              <a href="mailto:info@salonelegance.sk" class="flex items-center gap-2 text-primary-600 hover:text-primary-700 font-semibold transition-colors">
                <Icon name="mdi:email" class="text-xl" />
                info@salonelegance.sk
              </a>
            </div>
          </div>
        </div>

        <!-- Sidebar - Booking Summary -->
        <div class="lg:col-span-1">
          <BookingSummary 
            :service="form.service"
            :date="form.date"
            :time="form.time"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const form = ref({
  name: '',
  phone: '',
  email: '',
  service: '',
  date: '',
  time: '',
  message: ''
})

const isSubmitting = ref(false)
const submitMessage = ref('')
const submitSuccess = ref(false)

const services = [
  'Dámske strihanie',
  'Pánske strihanie',
  'Farbenie',
  'Melírovanie',
  'Keratínová kúra',
  'Svadobné účesy',
  'Detské strihanie',
  'Regeneračné procedúry'
]

const isFormValid = computed(() => {
  return form.value.name && 
         form.value.phone && 
         form.value.email && 
         form.value.service && 
         form.value.date && 
         form.value.time
})

const submitBooking = async () => {
  isSubmitting.value = true
  submitMessage.value = ''

  try {
    // Simulácia API call - v produkčnej verzii by ste tu volali skutočné API
    await new Promise(resolve => setTimeout(resolve, 1500))
    
    // Tu by ste normálne odoslali dáta na server
    console.log('Booking data:', form.value)
    
    submitSuccess.value = true
    submitMessage.value = 'Rezervácia bola úspešne odoslaná! Budeme vás kontaktovať v najbližšom čase.'
    
    // Reset formulára
    form.value = {
      name: '',
      phone: '',
      email: '',
      service: '',
      date: '',
      time: '',
      message: ''
    }
  } catch (error) {
    submitSuccess.value = false
    submitMessage.value = 'Nastala chyba pri odosielaní rezervácie. Skúste to prosím znova.'
  } finally {
    isSubmitting.value = false
    
    // Skryť správu po 5 sekundách
    setTimeout(() => {
      submitMessage.value = ''
    }, 5000)
  }
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

