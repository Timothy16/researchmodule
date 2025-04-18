<template>
    <li>
      <div class="block hover:bg-gray-50">
        <div class="px-4 py-4 sm:px-6">
          <div class="flex items-center justify-between">
            <div class="flex items-center">
              <i class="fas fa-file-alt h-5 w-5 text-gray-400 mr-3"></i>
              <p class="text-sm font-medium text-blue-600 truncate">{{ project.title }}</p>
            </div>
            <div class="ml-2 flex-shrink-0 flex">
              <p :class="statusClasses">{{ project.status }}</p>
            </div>
          </div>
          <div class="mt-2 sm:flex sm:justify-between">
            <div class="sm:flex">
              <p class="flex items-center text-sm text-gray-500">{{ project.dciNumber }}</p>
              <p class="mt-2 flex items-center text-sm text-gray-500 sm:mt-0 sm:ml-6">{{ project.course }}</p>
            </div>
            <div class="mt-2 flex items-center text-sm text-gray-500 sm:mt-0">
              <i class="fas fa-clock flex-shrink-0 mr-1.5 h-4 w-4 text-gray-400"></i>
              <p>{{ project.date }}</p>
              <button 
                v-if="project.hasViewButton"
                type="button" 
                class="ml-4 inline-flex items-center px-2.5 py-1.5 border border-transparent text-xs font-medium rounded text-blue-700 bg-blue-100 hover:bg-blue-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
              >
                View <i class="fas fa-arrow-right ml-1 h-3 w-3"></i>
              </button>
            </div>
          </div>
        </div>
      </div>
    </li>
  </template>
  
  <script setup>
  import { computed } from 'vue';
  
  const props = defineProps({
    project: {
      type: Object,
      required: true
    }
  });
  
  const statusClasses = computed(() => {
    const baseClasses = 'px-2 inline-flex text-xs leading-5 font-semibold rounded-full';
    
    const colorClasses = {
      green: 'bg-green-100 text-green-800',
      yellow: 'bg-yellow-100 text-yellow-800',
      red: 'bg-red-100 text-red-800'
    };
    
    return `${baseClasses} ${colorClasses[props.project.statusColor]}`;
  });
  </script>