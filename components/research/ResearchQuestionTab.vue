<!-- components/research/ResearchQuestionTab.vue -->
<template>
    <div>
      <h2 class="text-xl font-bold mb-4">Research Question</h2>
      <div class="bg-white rounded-lg border border-gray-200 p-6">
        <div class="flex items-center space-x-2 mb-4">
          <i class="fas fa-question-circle w-5 h-5 text-blue-600"></i>
          <h3 class="text-lg font-semibold">Research Question Generator</h3>
        </div>
        <div class="space-y-4">
          <textarea placeholder="Describe your research area or topic..." class="w-full h-32 p-3 border rounded-lg"></textarea>
          <button class="w-full py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">Generate Research Questions</button>
        </div>
      </div>
    </div>
  </template>