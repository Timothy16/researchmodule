<template>
    <div :class="version.isCurrent ? 'border border-blue-200 bg-blue-50 rounded-md p-4' : 'border border-gray-200 rounded-md p-4'">
      <div class="flex items-start justify-between">
        <div class="flex items-center">
          <i class="fas fa-code-commit h-5 w-5 text-gray-400 mr-2"></i>
          <div>
            <h4 class="text-sm font-medium text-gray-900">
              Version {{ version.number }}
              <span v-if="version.isCurrent" class="ml-2 px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-blue-100 text-blue-800">Current</span>
            </h4>
            <p class="mt-1 text-sm text-gray-500">{{ version.description }}</p>
            <p class="mt-1 text-xs text-gray-400">{{ version.date }}</p>
          </div>
        </div>
        <div class="ml-4">
          <button type="button" class="inline-flex items-center px-3 py-1 border border-gray-300 shadow-sm text-sm rounded-md text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
            View Version
          </button>
        </div>
      </div>
      
      <div v-if="version.changes && version.changes.length > 0" class="mt-3 text-sm">
        <details class="text-gray-500">
          <summary class="cursor-pointer hover:text-gray-700">Changes from previous version</summary>
          <div class="mt-2 pl-4 border-l-2 border-gray-200">
            <ul class="list-disc pl-4 space-y-1">
              <li v-for="(change, index) in version.changes" :key="index">{{ change }}</li>
            </ul>
          </div>
        </details>
      </div>
    </div>
  </template>
  
  <script setup>
  defineProps({
    version: {
      type: Object,
      required: true
    }
  });
  </script>