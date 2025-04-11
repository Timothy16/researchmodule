<template>
    <main class="flex-1 overflow-auto bg-gray-100">
      <div class="p-6">
        <div class="flex justify-between items-center mb-6">
          <h2 class="text-2xl font-semibold text-gray-800">Research Repository</h2>
          <button class="flex items-center space-x-2 px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm">
            <i class="fas fa-book-open w-5 h-5"></i>
            <span>Upload Research</span>
          </button>
        </div>
        <div class="bg-white rounded-lg p-4 shadow-sm mb-6">
          <div class="flex space-x-4 mb-6">
            <div class="flex-1 relative">
              <i class="fas fa-search absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-4 h-4"></i>
              <input 
                type="text" 
                placeholder="Search repositories..." 
                class="w-full pl-9 pr-4 py-2 border border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-300 text-sm"
              />
            </div>
            <button class="flex items-center space-x-2 px-4 py-2 border border-gray-200 rounded-lg hover:bg-gray-50 text-sm text-gray-600">
              <i class="fas fa-filter w-4 h-4"></i>
              <span>Filters</span>
            </button>
          </div>
          <div class="space-y-4">
            <div v-for="(research, index) in researchPapers" :key="index" class="flex items-center justify-between p-4 rounded-lg shadow-sm">
              <div class="flex-1">
                <div class="flex items-center space-x-3 mb-2">
                  <i class="fas fa-book-open w-5 h-5 text-blue-600"></i>
                  <h3 class="font-medium text-gray-800">{{ research.title }}</h3>
                </div>
                <p class="text-sm text-gray-500 mb-2">Authors: {{ research.authors }}</p>
                <div class="flex items-center space-x-2">
                  <span class="px-2 py-1 text-xs bg-blue-100 text-blue-700 rounded">
                    {{ research.category }}
                  </span>
                  <span class="px-2 py-1 text-xs bg-green-100 text-green-700 rounded">
                    {{ research.status }}
                  </span>
                </div>
              </div>
              <button class="flex items-center space-x-2 px-3 py-2 text-blue-600 hover:text-blue-700 text-sm font-medium">
                <i class="fas fa-download w-5 h-5"></i>
                <span>Download</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </main>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const researchPapers = ref([
    {
      title: 'Research Paper Title',
      authors: 'John Doe, Jane Smith',
      category: 'Computer Science',
      status: 'Peer Reviewed',
    },
    {
      title: 'Advances in Neural Networks',
      authors: 'Alice Brown, Bob Johnson',
      category: 'Machine Learning',
      status: 'Peer Reviewed',
    },
    {
      title: 'Ethics in AI Development',
      authors: 'Sarah Lee, David Kim',
      category: 'AI Ethics',
      status: 'Peer Reviewed',
    },
    {
      title: 'Natural Language Processing Techniques',
      authors: 'Emily Davis, Michael Chen',
      category: 'NLP',
      status: 'Peer Reviewed',
    },
    {
      title: 'Computer Vision Applications',
      authors: 'Laura Wilson, James Taylor',
      category: 'Computer Vision',
      status: 'Peer Reviewed',
    },
  ])
  </script>