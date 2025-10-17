<template>
  <section id="kontakt" class="py-20 md:py-32 bg-white">
    <div class="container mx-auto px-4">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-start">
        <!-- Contact Info -->
        <div>
          <div class="mb-12">
            <p class="section-subtitle">Kontakt</p>
            <h2 class="section-title">Navštívte nás</h2>
            <p class="text-lg text-secondary-600 mt-4">
              Tešíme sa na vašu návštevu v našom salóne
            </p>
          </div>

          <div class="space-y-8">
            <!-- Address -->
            <div class="flex items-start space-x-4">
              <div class="w-12 h-12 rounded-full bg-primary-100 flex items-center justify-center flex-shrink-0">
                <Icon name="mdi:map-marker" class="text-2xl text-primary-600" />
              </div>
              <div>
                <h3 class="font-semibold text-lg text-secondary-900 mb-1">Adresa</h3>
                <p class="text-secondary-600">
                  Hlavná ulica 123<br />
                  811 01 Bratislava<br />
                  Slovensko
                </p>
              </div>
            </div>

            <!-- Phone -->
            <div class="flex items-start space-x-4">
              <div class="w-12 h-12 rounded-full bg-primary-100 flex items-center justify-center flex-shrink-0">
                <Icon name="mdi:phone" class="text-2xl text-primary-600" />
              </div>
              <div>
                <h3 class="font-semibold text-lg text-secondary-900 mb-1">Telefón</h3>
                <a href="tel:+421901234567" class="text-secondary-600 hover:text-primary-600 transition-colors">
                  +421 901 234 567
                </a>
              </div>
            </div>

            <!-- Email -->
            <div class="flex items-start space-x-4">
              <div class="w-12 h-12 rounded-full bg-primary-100 flex items-center justify-center flex-shrink-0">
                <Icon name="mdi:email" class="text-2xl text-primary-600" />
              </div>
              <div>
                <h3 class="font-semibold text-lg text-secondary-900 mb-1">Email</h3>
                <a href="mailto:info@salonelegance.sk" class="text-secondary-600 hover:text-primary-600 transition-colors">
                  info@salonelegance.sk
                </a>
              </div>
            </div>

            <!-- Opening Hours -->
            <div class="flex items-start space-x-4">
              <div class="w-12 h-12 rounded-full bg-primary-100 flex items-center justify-center flex-shrink-0">
                <Icon name="mdi:clock-outline" class="text-2xl text-primary-600" />
              </div>
              <div>
                <h3 class="font-semibold text-lg text-secondary-900 mb-2">Otváracie hodiny</h3>
                <div class="space-y-1 text-secondary-600">
                  <p>Pondelok - Piatok: 9:00 - 18:00</p>
                  <p>Sobota: 9:00 - 14:00</p>
                  <p>Nedeľa: Zatvorené</p>
                </div>
              </div>
            </div>

            <!-- Social Media -->
            <div class="flex items-start space-x-4">
              <div class="w-12 h-12 rounded-full bg-primary-100 flex items-center justify-center flex-shrink-0">
                <Icon name="mdi:share-variant" class="text-2xl text-primary-600" />
              </div>
              <div>
                <h3 class="font-semibold text-lg text-secondary-900 mb-3">Sociálne siete</h3>
                <div class="flex space-x-4">
                  <a href="#" class="w-10 h-10 rounded-full bg-primary-600 hover:bg-primary-700 flex items-center justify-center text-white transition-colors">
                    <Icon name="mdi:facebook" class="text-xl" />
                  </a>
                  <a href="#" class="w-10 h-10 rounded-full bg-primary-600 hover:bg-primary-700 flex items-center justify-center text-white transition-colors">
                    <Icon name="mdi:instagram" class="text-xl" />
                  </a>
                  <a href="#" class="w-10 h-10 rounded-full bg-primary-600 hover:bg-primary-700 flex items-center justify-center text-white transition-colors">
                    <Icon name="mdi:youtube" class="text-xl" />
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Map -->
        <div class="lg:sticky lg:top-24">
          <div class="rounded-2xl overflow-hidden shadow-2xl h-[500px]">
            <iframe 
              src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2662.2391384083384!2d17.105850776779785!3d48.14557617123088!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x476c894e8684cd2d%3A0x403a61eedb089a0!2sBratislava%2C%20Slovakia!5e0!3m2!1sen!2s!4v1699999999999!5m2!1sen!2s"
              width="100%" 
              height="100%" 
              style="border:0;" 
              allowfullscreen="" 
              loading="lazy" 
              referrerpolicy="no-referrer-when-downgrade"
              class="grayscale hover:grayscale-0 transition-all duration-500"
            ></iframe>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
</script>

