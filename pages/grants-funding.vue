<template>
    <main class="flex-1 overflow-auto bg-gray-100">
      <div class="p-6">
        <h2 class="text-2xl font-semibold mb-6 text-gray-800">Research Grants & Funding</h2>
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
          <!-- Available Grants Organized by Project -->
          <div class="lg:col-span-2 space-y-6">
            <div v-for="(project, projectIndex) in projects" :key="projectIndex" class="bg-white rounded-lg p-4 shadow-sm">
              <h3 class="text-lg font-semibold mb-4 text-gray-800">{{ project.name }}</h3>
              <div v-for="(grant, grantIndex) in project.grants" :key="grantIndex" class="mb-4 p-4 bg-white rounded-lg shadow-sm border border-gray-200">
                <div class="flex items-start justify-between">
                  <div>
                    <h4 class="font-medium text-gray-800 mb-2">{{ grant.title }}</h4>
                    <p class="text-sm text-gray-500 mb-2">Amount: {{ grant.amount }}</p>
                    <div class="flex items-center space-x-4 text-sm text-gray-500">
                      <span class="flex items-center space-x-1">
                        <i class="fas fa-calendar w-4 h-4"></i>
                        <span>Deadline: {{ grant.deadline }}</span>
                      </span>
                      <span class="px-2 py-1 bg-green-100 text-green-700 rounded text-xs">
                        {{ grant.status }}
                      </span>
                    </div>
                  </div>
                  <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm">
                    Apply Now
                  </button>
                </div>
              </div>
            </div>
          </div>
  
          <!-- Sidebar -->
          <div class="space-y-4">
            <!-- Your Grant Status -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
              <h3 class="text-lg font-semibold mb-4 text-gray-800">Your Grant Status</h3>
              <div class="space-y-3">
                <div class="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                  <div class="flex items-center space-x-3">
                    <i class="fas fa-dollar-sign w-5 h-5 text-green-600"></i>
                    <span class="text-gray-800">Active Grants</span>
                  </div>
                  <span class="font-semibold text-gray-800">{{ grantStatus.activeGrants }}</span>
                </div>
                <div class="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                  <div class="flex items-center space-x-3">
                    <i class="fas fa-chart-line w-5 h-5 text-blue-600"></i>
                    <span class="text-gray-800">Success Rate</span>
                  </div>
                  <span class="font-semibold text-gray-800">{{ grantStatus.successRate }}</span>
                </div>
                <div class="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                  <div class="flex items-center space-x-3">
                    <i class="fas fa-award w-5 h-5 text-yellow-600"></i>
                    <span class="text-gray-800">Total Awarded</span>
                  </div>
                  <span class="font-semibold text-gray-800">{{ grantStatus.totalAwarded }}</span>
                </div>
              </div>
            </div>
  
            <!-- Recommended Grants -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
              <h3 class="text-lg font-semibold mb-4 text-gray-800">Recommended Grants</h3>
              <div class="space-y-3">
                <div v-for="(recommendation, index) in recommendedGrants" :key="index" class="p-3 border border-gray-200 rounded-lg">
                  <h4 class="font-medium text-gray-800 mb-1">{{ recommendation.title }}</h4>
                  <p class="text-sm text-gray-500">Matches your profile: {{ recommendation.matchPercentage }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const projects = ref([
    {
      name: 'Project Alpha',
      grants: [
        {
          title: 'AI Research Innovation Grant',
          amount: '$50,000 - $100,000',
          deadline: 'Mar 30, 2024',
          status: 'Open',
        },
        {
          title: 'Tech Advancement Fund',
          amount: '$30,000 - $75,000',
          deadline: 'Apr 15, 2024',
          status: 'Open',
        },
      ],
    },
    {
      name: 'Project Beta',
      grants: [
        {
          title: 'Data Science Research Grant',
          amount: '$40,000 - $90,000',
          deadline: 'May 10, 2024',
          status: 'Open',
        },
      ],
    },
    {
      name: 'Project Gamma',
      grants: [
        {
          title: 'Machine Learning Innovation Grant',
          amount: '$60,000 - $120,000',
          deadline: 'Jun 20, 2024',
          status: 'Open',
        },
        {
          title: 'AI Ethics Research Fund',
          amount: '$25,000 - $50,000',
          deadline: 'Jul 5, 2024',
          status: 'Open',
        },
      ],
    },
  ])
  
  const grantStatus = ref({
    activeGrants: 2,
    successRate: '75%',
    totalAwarded: '$150,000',
  })
  
  const recommendedGrants = ref([
    { title: 'Research Excellence Grant', matchPercentage: '95%' },
    { title: 'Innovation in AI Grant', matchPercentage: '90%' },
    { title: 'Sustainable Tech Fund', matchPercentage: '85%' },
  ])
  </script>