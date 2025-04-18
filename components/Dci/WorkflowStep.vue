<template>
    <li :class="{ 'relative pb-8': !isLast, 'relative': isLast }">
      <!-- Vertical Line -->
      <div 
        v-if="!isLast" 
        class="absolute top-1/2 left-4 -ml-px h-full w-0.5 bg-gray-300 transform -translate-y-1/2" 
        aria-hidden="true"
      ></div>
      
      <!-- Step Content -->
      <div class="group relative flex items-start">
        <!-- Step Circle -->
        <span class="h-9 flex items-center justify-center">
          <span 
            :class="[ 
              'relative z-10 w-8 h-8 flex items-center justify-center rounded-full',
              {
                'bg-green-500': step.state === 'completed',
                'bg-blue-600': step.state === 'current',
                'bg-gray-300': step.state === 'upcoming'
              }
            ]"
          >
            <!-- Icon -->
            <i 
              v-if="step.state === 'completed'" 
              class="fas fa-check text-white text-sm"
            ></i>
            <i 
              v-else 
              class="fas fa-clock text-sm"
              :class="{
                'text-white': step.state === 'current',
                'text-gray-500': step.state === 'upcoming'
              }"
            ></i>
          </span>
        </span>
  
        <!-- Step Text -->
        <span class="ml-4 min-w-0 flex flex-col">
          <span class="text-sm font-medium text-gray-900">{{ step.name }}</span>
          <span class="text-sm text-gray-500">{{ step.status }}</span>
        </span>
      </div>
    </li>
  </template>
  
  
  <script setup>
  defineProps({
    step: {
      type: Object,
      required: true
    },
    isLast: {
      type: Boolean,
      default: false
    }
  });
  </script>