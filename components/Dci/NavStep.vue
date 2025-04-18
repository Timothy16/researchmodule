<template>
    <li :class="isLast ? 'relative' : 'pr-8 sm:pr-20 relative'">
      <div>
        <div class="absolute inset-0 flex items-center" aria-hidden="true">
          <div class="h-0.5 w-full" :class="isComplete ? 'bg-blue-600' : 'bg-gray-200'"></div>
        </div>
        <button
          class="relative w-8 h-8 flex items-center justify-center border-2 rounded-full"
          :class="{
            'bg-blue-600 border-blue-600 text-white': isComplete,
            'border-blue-600': isActive && !isComplete,
            'border-gray-300 hover:border-gray-400': !isActive && !isComplete
          }"
          @click="$emit('click')"
        >
          <template v-if="isComplete">
            <svg class="w-4 h-4 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7" />
            </svg>
          </template>
          <template v-else>
            <span class="h-2.5 w-2.5 rounded-full"
              :class="{
                'bg-blue-600': isActive,
                'bg-transparent group-hover:bg-gray-300': !isActive
              }"
            ></span>
          </template>
          <span class="sr-only">{{ step.name }}</span>
        </button>
      </div>
      <div class="hidden sm:block absolute top-0 translate-y-10 mt-0.5">
        <div class="font-medium text-sm text-gray-500">{{ step.name }}</div>
      </div>
    </li>
  </template>
  
  <script setup>
  defineProps({
    step: Object,
    isActive: Boolean,
    isComplete: Boolean,
    isLast: Boolean
  });
  defineEmits(['click']);
  </script>
  