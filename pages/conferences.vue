<template>
    <main class="flex-1 overflow-auto bg-gray-100">
      <div class="p-6">
        <h2 class="text-2xl font-semibold mb-6 text-gray-800">Academic Conferences</h2>
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
          <!-- Conference List -->
          <div class="lg:col-span-2 space-y-4">
            <div class="bg-white rounded-lg p-4 shadow-sm">
              <div class="relative mb-4">
                <i class="fas fa-search absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-4 h-4"></i>
                <input 
                  type="text" 
                  placeholder="Search conferences..." 
                  class="w-full pl-9 pr-4 py-2 border border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-300 text-sm"
                />
              </div>
            </div>
            <div v-for="(conference, index) in conferences" :key="index" class="bg-white rounded-lg p-4 shadow-sm">
              <h4 class="font-medium text-gray-800 mb-2">{{ conference.title }}</h4>
              <div class="space-y-2 text-sm text-gray-500">
                <div class="flex items-center space-x-2">
                  <i class="fas fa-calendar w-4 h-4"></i>
                  <span>{{ conference.date }}</span>
                </div>
                <div class="flex items-center space-x-2">
                  <i class="fas fa-map-pin w-4 h-4"></i>
                  <span>{{ conference.location }}</span>
                </div>
                <div class="flex items-center space-x-2">
                  <i class="fas fa-globe w-4 h-4"></i>
                  <span>{{ conference.type }}</span>
                </div>
              </div>
              <button class="mt-4 text-blue-600 hover:text-blue-700 text-sm font-medium">
                View Details
              </button>
            </div>
          </div>
  
          <!-- Sidebar -->
          <div class="space-y-4">
            <!-- Your Submissions -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
              <h3 class="text-lg font-semibold mb-4 text-gray-800">Your Submissions</h3>
              <div class="space-y-3">
                <div v-for="(submission, index) in submissions" :key="index" class="p-3 border border-gray-200 rounded-lg">
                  <h4 class="font-medium text-gray-800 mb-1">{{ submission.title }}</h4>
                  <p class="text-sm text-gray-500">Status: {{ submission.status }}</p>
                </div>
              </div>
            </div>
  
            <!-- Upcoming Deadlines -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
              <h3 class="text-lg font-semibold mb-4 text-gray-800">Upcoming Deadlines</h3>
              <div class="space-y-3">
                <div v-for="(deadline, index) in deadlines" :key="index" class="flex items-start space-x-3">
                  <i class="fas fa-user w-5 h-5 text-gray-400"></i>
                  <div>
                    <p class="font-medium text-gray-800">{{ deadline.title }}</p>
                    <p class="text-sm text-gray-500">{{ deadline.due }}</p>
                  </div>
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
  
  const conferences = ref([
    {
      title: 'International Conference on AI Research',
      date: 'June 15-18, 2024',
      location: 'San Francisco, CA',
      type: 'Hybrid Event',
    },
    {
      title: 'International Conference on AI Research',
      date: 'June 15-18, 2024',
      location: 'San Francisco, CA',
      type: 'Hybrid Event',
    },
    {
      title: 'International Conference on AI Research',
      date: 'June 15-18, 2024',
      location: 'San Francisco, CA',
      type: 'Hybrid Event',
    },
  ])
  
  const submissions = ref([
    { title: 'Paper Title', status: 'Under Review' },
    { title: 'Paper Title', status: 'Under Review' },
  ])
  
  const deadlines = ref([
    { title: 'Paper Submission', due: 'Due in 5 days' },
    { title: 'Paper Submission', due: 'Due in 5 days' },
    { title: 'Paper Submission', due: 'Due in 5 days' },
  ])
</script>