<template>
    <div>
      <h4 class="text-sm font-medium text-gray-900">{{ title }}</h4>
      <div class="mt-1 p-3 bg-gray-50 rounded-md">
        <p class="text-xs text-gray-800 font-mono">{{ content }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  defineProps({
    title: {
      type: String,
      required: true
    },
    content: {
      type: String,
      required: true
    }
  });
  </script>