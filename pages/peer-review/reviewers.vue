<template>
   <main class="flex-1 overflow-auto p-6">
  <div class="max-w-6xl mx-auto">
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-2xl font-semibold text-gray-800">Reviewers</h2>
      <div class="flex space-x-4">
        <div class="relative">
          <i class="fas fa-search absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"></i>
          <input type="text" placeholder="Search reviewers..." class="pl-10 pr-4 py-2 border border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
        </div>
        <button class="flex items-center px-4 py-2 border border-gray-200 rounded-lg hover:bg-gray-50">
          <i class="fas fa-filter w-5 h-5 mr-2"></i>Filter
        </button>
      </div>
    </div>

    <div class="grid gap-6">
      <!-- Reviewer 1 -->
      <div class="bg-white p-6 rounded-lg border border-gray-200">
        <div class="flex justify-between items-start">
          <div>
            <h3 class="text-lg font-semibold text-gray-800">Dr. Sarah Johnson</h3>
            <p class="text-gray-600">Computer Science</p>
            <div class="flex items-center mt-2">
              
              <span class="text-gray-600">142 reviews</span>
            </div>
          </div>
          <span class="px-3 py-1 rounded-full text-sm bg-green-100 text-green-800">Available</span>
        </div>
        <div class="mt-4">
          <h4 class="text-sm font-medium text-gray-700 mb-2">Expertise</h4>
          <div class="flex flex-wrap gap-2">
            <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-sm">Machine Learning</span>
            <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-sm">AI Ethics</span>
            <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-sm">Data Science</span>
          </div>
        </div>
      </div>

      <!-- Reviewer 2 -->
      <div class="bg-white p-6 rounded-lg border border-gray-200">
        <div class="flex justify-between items-start">
          <div>
            <h3 class="text-lg font-semibold text-gray-800">Prof. Michael Chen</h3>
            <p class="text-gray-600">Information Systems</p>
            <div class="flex items-center mt-2">
              
              
              <span class="text-gray-600">89 reviews</span>
            </div>
          </div>
          <span class="px-3 py-1 rounded-full text-sm bg-green-100 text-green-800">Available</span>
        </div>
        <div class="mt-4">
          <h4 class="text-sm font-medium text-gray-700 mb-2">Expertise</h4>
          <div class="flex flex-wrap gap-2">
            <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-sm">Database Systems</span>
            <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-sm">Cloud Computing</span>
            <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-sm">Software Engineering</span>
          </div>
        </div>
      </div>

      <!-- Reviewer 3 -->
      <div class="bg-white p-6 rounded-lg border border-gray-200">
        <div class="flex justify-between items-start">
          <div>
            <h3 class="text-lg font-semibold text-gray-800">Dr. Emily Williams</h3>
            <p class="text-gray-600">Digital Media</p>
            <div class="flex items-center mt-2">
              
             
              <span class="text-gray-600">67 reviews</span>
            </div>
          </div>
          <span class="px-3 py-1 rounded-full text-sm bg-gray-100 text-gray-800">Unavailable</span>
        </div>
        <div class="mt-4">
          <h4 class="text-sm font-medium text-gray-700 mb-2">Expertise</h4>
          <div class="flex flex-wrap gap-2">
            <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-sm">UX Research</span>
            <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-sm">HCI</span>
            <span class="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-sm">Digital Ethics</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</main>
</template>
  
<script setup>
  definePageMeta({
    layout: 'peer'
  })
</script>