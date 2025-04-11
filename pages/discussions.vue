<template>
    <main class="flex-1 overflow-auto bg-gray-100 p-6">
      <div class="max-w-6xl mx-auto">
        <div class="flex justify-between items-center mb-6">
          <h2 class="text-2xl font-semibold text-gray-800">Discussions</h2>
          <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm">
            New Discussion
          </button>
        </div>
        <div class="grid grid-cols-1 lg:grid-cols-4 gap-6">
          <!-- Discussion List -->
          <div class="lg:col-span-3">
            <div class="space-y-4">
              <div v-for="(discussion, index) in discussions" :key="index" class="bg-white p-6 rounded-lg shadow-sm">
                <div class="flex justify-between items-start">
                  <div>
                    <h3 class="text-lg font-semibold text-gray-800 hover:text-blue-600 cursor-pointer">
                      {{ discussion.title }}
                    </h3>
                    <p class="text-sm text-gray-500 mt-1">Started by {{ discussion.startedBy }}</p>
                  </div>
                  <span class="px-3 py-1 bg-blue-100 text-blue-800 rounded-full text-xs">
                    {{ discussion.category }}
                  </span>
                </div>
                <div class="mt-4 flex items-center space-x-6 text-sm text-gray-500">
                  <div class="flex items-center">
                    <i class="fas fa-users w-4 h-4 mr-1"></i>
                    {{ discussion.participants }} participants
                  </div>
                  <div class="flex items-center">
                    <i class="fas fa-comment w-4 h-4 mr-1"></i>
                    {{ discussion.replies }} replies
                  </div>
                  <div>Last activity {{ discussion.lastActivity }}</div>
                </div>
              </div>
            </div>
          </div>
  
          <!-- Sidebar (Categories) -->
          <div class="lg:col-span-1">
            <div class="bg-white p-6 rounded-lg shadow-sm">
              <h3 class="font-semibold text-gray-800 mb-4">Categories</h3>
              <div class="space-y-2">
                <button v-for="(category, index) in categories" :key="index" class="flex items-center w-full px-3 py-2 text-gray-600 hover:bg-gray-50 rounded-lg">
                  <i class="fas fa-tag w-4 h-4 mr-2"></i>
                  {{ category }}
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const discussions = ref([
    {
      title: 'Best practices for implementing neural networks in healthcare applications',
      startedBy: 'Dr. Emily Williams',
      category: 'Machine Learning',
      participants: 12,
      replies: 45,
      lastActivity: '10 minutes ago',
    },
    {
      title: 'Ethics in AI: Addressing bias in training data',
      startedBy: 'Prof. David Lee',
      category: 'AI Ethics',
      participants: 8,
      replies: 23,
      lastActivity: '1 hour ago',
    },
    {
      title: 'New approaches to natural language processing',
      startedBy: 'Dr. Sarah Johnson',
      category: 'NLP',
      participants: 15,
      replies: 67,
      lastActivity: '2 hours ago',
    },
  ])
  
  const categories = ref([
    'Machine Learning',
    'AI Ethics',
    'Data Science',
    'NLP',
    'Computer Vision',
  ])
  </script>