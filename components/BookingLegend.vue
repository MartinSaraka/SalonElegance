<template>
  <div class="bg-secondary-50 rounded-xl p-6 mt-6">
    <h4 class="font-semibold text-secondary-900 mb-4 flex items-center">
      <Icon name="mdi:information" class="text-xl mr-2 text-primary-600" />
      Legenda
    </h4>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
      <div class="flex items-center space-x-3">
        <div class="w-8 h-8 rounded-lg bg-primary-600 flex-shrink-0"></div>
        <span class="text-sm text-secondary-700">Vybraný deň</span>
      </div>
      <div class="flex items-center space-x-3">
        <div class="w-8 h-8 rounded-lg bg-secondary-50 border-2 border-secondary-200 flex-shrink-0"></div>
        <span class="text-sm text-secondary-700">Dostupné dni</span>
      </div>
      <div class="flex items-center space-x-3">
        <div class="w-8 h-8 rounded-lg bg-white text-secondary-300 flex items-center justify-center text-xs flex-shrink-0">
          <span class="line-through">X</span>
        </div>
        <span class="text-sm text-secondary-700">Zatvorené</span>
      </div>
      <div class="flex items-center space-x-3">
        <div class="w-8 h-8 rounded-lg bg-white text-secondary-300 flex items-center justify-center text-xs opacity-50 flex-shrink-0">
          X
        </div>
        <span class="text-sm text-secondary-700">Obsadené</span>
      </div>
    </div>
    
    <div class="mt-4 pt-4 border-t border-secondary-200">
      <p class="text-sm text-secondary-600 flex items-start">
        <Icon name="mdi:lightbulb-on" class="text-primary-600 mr-2 mt-0.5 flex-shrink-0" />
        <span><strong>Tip:</strong> Kliknite na zelený deň v kalendári, aby ste videli dostupné časové sloty.</span>
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
</script>

