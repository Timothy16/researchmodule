<template>
 <main class="flex-1 overflow-auto p-6">
  <div class="max-w-6xl mx-auto">
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-2xl font-semibold text-gray-800">Reviews</h2>
      <div class="flex space-x-4">
        <select class="px-4 py-2 border border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
          <option>All Reviews</option>
          <option>In Progress</option>
          <option>Completed</option>
          <option>Pending</option>
        </select>
      </div>
    </div>

    <div class="grid gap-6">
      <!-- Review 1 -->
      <div class="bg-white p-6 rounded-lg border border-gray-200">
        <div class="flex justify-between items-start">
          <div>
            <h3 class="text-lg font-semibold text-gray-800">Machine Learning Applications in Healthcare</h3>
            <p class="text-gray-600">by Dr. James Wilson</p>
          </div>
          <span class="px-3 py-1 rounded-full text-sm bg-blue-100 text-blue-800">In Progress</span>
        </div>
        <div class="mt-4 flex items-center space-x-6">
          <div class="flex items-center">
            <i class="fas fa-clock w-5 h-5 text-gray-400 mr-2"></i>
            <span class="text-gray-600">Due 2024-03-15</span>
          </div>
          <div class="flex items-center">
            <i class="fas fa-check-circle w-5 h-5 text-gray-400 mr-2"></i>
            <span class="text-gray-600">1/3 Reviews Complete</span>
          </div>
        </div>
      </div>

      <!-- Review 2 -->
      <div class="bg-white p-6 rounded-lg border border-gray-200">
        <div class="flex justify-between items-start">
          <div>
            <h3 class="text-lg font-semibold text-gray-800">Blockchain Security Protocols</h3>
            <p class="text-gray-600">by Prof. Lisa Chen</p>
          </div>
          <span class="px-3 py-1 rounded-full text-sm bg-green-100 text-green-800">Completed</span>
        </div>
        <div class="mt-4 flex items-center space-x-6">
          <div class="flex items-center">
            <i class="fas fa-clock w-5 h-5 text-gray-400 mr-2"></i>
            <span class="text-gray-600">Due 2024-02-28</span>
          </div>
          <div class="flex items-center">
            <i class="fas fa-check-circle w-5 h-5 text-gray-400 mr-2"></i>
            <span class="text-gray-600">2/2 Reviews Complete</span>
          </div>
        </div>
      </div>

      <!-- Review 3 -->
      <div class="bg-white p-6 rounded-lg border border-gray-200">
        <div class="flex justify-between items-start">
          <div>
            <h3 class="text-lg font-semibold text-gray-800">Neural Network Optimization</h3>
            <p class="text-gray-600">by Dr. Robert Brown</p>
          </div>
          <span class="px-3 py-1 rounded-full text-sm bg-yellow-100 text-yellow-800">Pending</span>
        </div>
        <div class="mt-4 flex items-center space-x-6">
          <div class="flex items-center">
            <i class="fas fa-clock w-5 h-5 text-gray-400 mr-2"></i>
            <span class="text-gray-600">Due 2024-03-20</span>
          </div>
          <div class="flex items-center">
            <i class="fas fa-check-circle w-5 h-5 text-gray-400 mr-2"></i>
            <span class="text-gray-600">0/3 Reviews Complete</span>
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