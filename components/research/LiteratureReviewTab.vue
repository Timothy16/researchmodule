<!-- components/research/LiteratureReviewTab.vue -->
<template>
    <div>
      <h2 class="text-xl font-bold mb-4">Literature Review</h2>
      <div class="bg-white rounded-lg border border-gray-200 p-6">
        <div class="flex items-center space-x-2 mb-4">
          <i class="fas fa-book-open w-5 h-5 text-blue-600"></i>
          <h3 class="text-lg font-semibold">Literature Review Assistant</h3>
        </div>
        <textarea placeholder="Paste your text here for analysis..." class="w-full h-32 p-3 border rounded-lg mb-4"></textarea>
        <button class="w-full py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">Analyze Text</button>
      </div>
    </div>
  </template>