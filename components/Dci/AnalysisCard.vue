<template>
    <div class="bg-white shadow overflow-hidden sm:rounded-lg">
      <!-- Card Header -->
      <div :class="`px-4 py-5 sm:px-6 bg-${color}-50`">
        <h3 class="text-lg font-medium leading-6 text-gray-900 flex items-center">
          <i :class="`fas ${icon} w-5 h-5 text-${color}-500 mr-2`"></i>
          {{ title }}
        </h3>
      </div>
      
      <!-- Card Content -->
      <div class="px-4 py-5 sm:p-6">
        <div class="flex items-center justify-center">
          <div :class="`text-5xl font-bold text-${color}-600`">{{ score }}</div>
        </div>
        <div class="mt-4 text-sm text-gray-500">{{ description }}</div>
      </div>
    </div>
  </template>
  
  <script setup>
  defineProps({
    title: {
      type: String,
      required: true
    },
    score: {
      type: String,
      required: true
    },
    color: {
      type: String,
      default: 'blue',
      validator: (value) => ['green', 'yellow', 'blue', 'red', 'gray'].includes(value)
    },
    icon: {
      type: String,
      required: true
    },
    description: {
      type: String,
      default: ''
    }
  });
  </script>