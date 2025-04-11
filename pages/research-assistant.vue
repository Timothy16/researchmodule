<!-- pages/lecturer/research-assistant.vue -->
<template>
   
      <div>
        <!-- Header Section -->
        <div class="mb-6">
          <h1 class="text-3xl font-bold mb-2 flex items-center text-gray-800">
            <i class="fas fa-flask text-blue-600 mr-2"></i>
            Research Assistant
          </h1>
          <p class="text-gray-600">
            Generate topics, conduct literature reviews, and improve your research documents.
          </p>
        </div>
        
        <!-- Main screen  -->
        <div class="flex flex-col h-full">
          <!-- Main Panel -->
          <div class="w-full relative flex flex-col overflow-hidden bg-white rounded-lg shadow-md">
            <!-- Tabs Navigation -->
            <div class="border-b border-gray-200 bg-gray-50">
              <div class="flex overflow-x-auto">
                <!-- Tabs -->
                <button 
                  v-for="tab in tabs" 
                  :key="tab.id"
                  @click="activeTab = tab.id"
                  class="px-4 py-3 flex items-center whitespace-nowrap"
                  :class="activeTab === tab.id ? 
                    'border-b-2 border-blue-600 text-blue-600 font-medium' : 
                    'text-gray-700 hover:bg-gray-100'"
                >
                  <i :class="[tab.icon, 'mr-2']"></i>
                  {{ tab.label }}
                </button>
              </div>
            </div>
            
            <!-- Tab Content -->
            <div class="flex-grow overflow-y-auto p-6">
              <!-- Topic Generator Tab -->
              <TopicGeneratorTab v-if="activeTab === 'topicGenerator'" />
              
              <!-- Literature Review Tab -->
              <LiteratureReviewTab v-if="activeTab === 'literatureReview'" />
              
              <!-- Research Question Tab -->
              <ResearchQuestionTab v-if="activeTab === 'researchQuestion'" />
              
              <!-- Upload Document Tab -->
              <UploadDocumentTab v-if="activeTab === 'uploadDocument'" />
              
              <!-- AI Grammar Check Tab -->
              <GrammarCheckTab v-if="activeTab === 'grammarCheck'" />
              
              <!-- Plagiarism Tab -->
              <PlagiarismTab v-if="activeTab === 'plagiarism'" />
            </div>
          </div>
        </div>
      </div>
  
</template>
  
<script setup>
  import { ref } from 'vue';
  import TopicGeneratorTab from '@/components/research/TopicGeneratorTab.vue';
  import LiteratureReviewTab from '@/components/research/LiteratureReviewTab.vue';
  import ResearchQuestionTab from '@/components/research/ResearchQuestionTab.vue';
  import UploadDocumentTab from '@/components/research/UploadDocumentTab.vue';
  import GrammarCheckTab from '@/components/research/GrammarCheckTab.vue';
  import PlagiarismTab from '@/components/research/PlagiarismTab.vue';
  
  // Active tab tracking
  const activeTab = ref('topicGenerator');
  
  // Tab definitions
  const tabs = [
    { id: 'topicGenerator', label: 'Topic Generator', icon: 'fas fa-lightbulb' },
    { id: 'literatureReview', label: 'Literature Review', icon: 'fas fa-book' },
    { id: 'researchQuestion', label: 'Research Question', icon: 'fas fa-question-circle' },
    { id: 'uploadDocument', label: 'Upload Document', icon: 'fas fa-file-upload' },
    { id: 'grammarCheck', label: 'AI Grammar Check', icon: 'fas fa-spell-check' },
    { id: 'plagiarism', label: 'Plagiarism', icon: 'fas fa-shield-alt' },
  ];
  </script>
  
  <style scoped>
  /* Smooth transitions for tab interactions */
  button {
    transition: background-color 0.2s, color 0.2s;
  }
  
  /* Improved focus states for accessibility */
  button:focus, input:focus, textarea:focus, select:focus {
    outline: none;
    box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.3);
  }
  
  /* Mobile styles */
  @media (max-width: 767px) {
    /* Make the tab container scrollable on small screens */
    .overflow-x-auto {
      -webkit-overflow-scrolling: touch;
      scrollbar-width: none; /* Firefox */
      -ms-overflow-style: none; /* IE and Edge */
    }
    
    .overflow-x-auto::-webkit-scrollbar {
      display: none; /* Chrome, Safari, Opera */
    }
    
    /* Adjust button sizes for better touch targets */
    button {
      min-height: 44px; /* Minimum touch target size */
    }
  }
  </style>