<template>
    <main class="flex-1 overflow-auto p-6">
  <div class="max-w-4xl mx-auto">
    <h2 class="text-2xl font-semibold text-gray-800 mb-6">Submit Paper</h2>

    <div class="bg-white p-8 rounded-lg border border-gray-200 mb-6">
      <h3 class="text-lg font-semibold text-gray-800 mb-4">Choose Review Mode</h3>
      <div class="grid gap-4">
        <label class="p-4 border rounded-lg cursor-pointer border-blue-500 bg-blue-50">
          <div class="flex items-start">
            <input type="radio" name="reviewMode" class="mt-1" value="double-blind" checked="">
            <div class="ml-3">
              <span class="font-medium text-gray-800">Double-blind Review</span>
              <p class="text-sm text-gray-600 mt-1">Neither author nor reviewer knows each other's identity. Maximum objectivity.</p>
            </div>
          </div>
        </label>
        <label class="p-4 border rounded-lg cursor-pointer border-gray-200">
          <div class="flex items-start">
            <input type="radio" name="reviewMode" class="mt-1" value="single-blind">
            <div class="ml-3">
              <span class="font-medium text-gray-800">Single-blind Review</span>
              <p class="text-sm text-gray-600 mt-1">Reviewer knows author's identity, but author doesn't know reviewer.</p>
            </div>
          </div>
        </label>
        <label class="p-4 border rounded-lg cursor-pointer border-gray-200">
          <div class="flex items-start">
            <input type="radio" name="reviewMode" class="mt-1" value="open">
            <div class="ml-3">
              <span class="font-medium text-gray-800">Open Review</span>
              <p class="text-sm text-gray-600 mt-1">Both identities and comments are visible. Promotes transparency and open dialogue.</p>
            </div>
          </div>
        </label>
        
        <div class="mt-4">
          <label class="block text-sm font-medium text-gray-700 mb-2">Invite Reviewers by Email</label>
          <div class="flex items-center">
            <div class="flex-grow">
              <input type="text" class="w-full px-4 py-2 border border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="Enter email addresses separated by commas">
            </div>
            <!-- <button class="ml-2 px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">
              <i class="fas fa-paper-plane mr-2"></i>Invite
            </button> -->
          </div>
          <p class="text-sm text-gray-500 mt-1">You can invite specific reviewers to evaluate your paper by adding their email addresses here.</p>
          
          <div class="mt-3">
            <div class="flex flex-wrap gap-2">
              <div class="bg-blue-50 text-blue-800 px-3 py-1 rounded-full flex items-center">
                reviewer1@example.com
                <button class="ml-1 text-blue-500 hover:text-blue-700">
                  <i class="fas fa-times-circle"></i>
                </button>
              </div>
              <div class="bg-blue-50 text-blue-800 px-3 py-1 rounded-full flex items-center">
                reviewer2@example.com
                <button class="ml-1 text-blue-500 hover:text-blue-700">
                  <i class="fas fa-times-circle"></i>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="bg-white p-8 rounded-lg border border-gray-200">
      <h3 class="text-lg font-semibold text-gray-800 mb-4">Paper Details</h3>
      <div class="space-y-6">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Paper Title</label>
          <input type="text" class="w-full px-4 py-2 border border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="Enter the title of your paper">
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Abstract</label>
          <textarea class="w-full px-4 py-2 border border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" rows="4" placeholder="Enter your paper's abstract"></textarea>
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Keywords</label>
          <input type="text" class="w-full px-4 py-2 border border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="Enter keywords separated by commas">
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Upload Paper</label>
          <div class="border-2 border-dashed border-gray-200 rounded-lg p-8">
            <div class="flex flex-col items-center">
              <i class="fas fa-upload w-12 h-12 text-gray-400 mb-4"></i>
              <p class="text-gray-600 text-center mb-4">Drag and drop your paper here, or click to select file</p>
              <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">Select File</button>
            </div>
          </div>
        </div>
        <div class="flex justify-end">
          <button class="px-6 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700">Submit Paper</button>
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