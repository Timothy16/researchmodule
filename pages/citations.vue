<template>
  <div>
    <div class="flex justify-between items-center mb-6">
      <h1 class="text-2xl font-bold text-gray-800">Citation Manager</h1>
      <button @click="showModal = true" class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-md flex items-center">
        <i class="fas fa-plus mr-2"></i> Add Citation
      </button>
    </div>
    
    <!-- Main Content Area -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
      <!-- Citation List -->
      <div class="md:col-span-2 bg-white rounded-lg border border-gray-200 p-6">
        <!-- Search Bar -->
        <div class="mb-4 relative">
          <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
            <i class="fas fa-search text-gray-400"></i>
          </div>
          <input type="text" placeholder="Search citations..." 
                  class="block w-full pl-10 pr-3 py-2 border border-gray-300 rounded-md leading-5 bg-white focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 text-sm">
        </div>
        
        <!-- Citations -->
        <div v-for="(citation, index) in citations" :key="index"
              class=" space-y-4  ">
          <div class="flex mb-3 items-center justify-between p-4 border rounded-lg">
            <div>
              <h4 class="font-medium mb-1">{{ citation.title }}</h4>
              <p class="text-sm text-gray-600">Authors: {{ citation.authors }}</p>
            </div>
            <button class="text-blue-600 hover:text-blue-800 flex items-center">
              <i class="fas fa-download mr-1"></i> Export
            </button>
          </div>
        </div>
      </div>
      
      <!-- Right Sidebar -->
      <div class="bg-white rounded-md shadow p-4 h-fit">
        <h2 class="text-lg font-medium mb-4">Citation Formats</h2>
        
        <div class="space-y-4">
          <button v-for="(format, index) in formats" :key="index"
          class="flex items-center w-full space-x-3 p-3 border rounded-lg">
            <i class="fas fa-file-alt text-blue-600 mr-3"></i>
            <span>{{ format }} Format</span>
          </button>
        </div>
      </div>
    </div>
    <div v-if="showModal" class="fixed inset-0 bg-gray-600 bg-opacity-50 flex items-center justify-center z-50">
  <div class="bg-white rounded-lg p-8 w-full max-w-2xl">
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-2xl font-semibold">Add New Citation</h2>
      <button @click="showModal = false" class="text-gray-500 hover:text-gray-700">
        <i class="fas fa-times"></i>
      </button>
    </div>
    
    <form @submit.prevent="addCitation">
      <div class="mb-6">
        <label class="block text-sm font-medium text-gray-700 mb-2">Citation Input Method</label>
        <div class="flex space-x-4">
          <label class="flex items-center">
            <input 
              type="radio" 
              v-model="inputMethod" 
              value="project" 
              class="mr-2" 
            />
            Select Project
          </label>
          <label class="flex items-center">
            <input 
              type="radio" 
              v-model="inputMethod" 
              value="text" 
              class="mr-2" 
            />
            Paste Citation Text
          </label>
        </div>
      </div>

      <div v-if="inputMethod === 'project'" class="mb-6">
        <label for="project" class="block text-sm font-medium text-gray-700 mb-2">Select Project</label>
        <select 
          v-model="newCitation.project"
          id="project"
          class="w-full border border-gray-300 rounded-md px-4 py-3 focus:outline-none focus:ring-2 focus:ring-blue-500"
          :disabled="inputMethod !== 'project'"
        >
          <option value="">Select a project</option>
          <option v-for="project in projects" :key="project.id" :value="project.id">
            {{ project.name }}
          </option>
        </select>
      </div>
      
      <div v-if="inputMethod === 'text'" class="mb-6">
        <label for="citationText" class="block text-sm font-medium text-gray-700 mb-2">Citation Text</label>
        <textarea
          v-model="newCitation.text"
          id="citationText"
          rows="6"
          class="w-full border border-gray-300 rounded-md px-4 py-3 focus:outline-none focus:ring-2 focus:ring-blue-500"
          placeholder="Paste or type your citation here..."
          :disabled="inputMethod !== 'text'"
        ></textarea>
      </div>
      
      <div class="flex justify-end space-x-3">
        <button 
          type="button" 
          @click="showModal = false"
          class="px-6 py-2 text-gray-600 border border-gray-300 rounded-md hover:bg-gray-50"
        >
          Cancel
        </button>
        <button 
          type="submit"
          class="px-6 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700"
          :disabled="!isFormValid"
        >
          Add Citation
        </button>
      </div>
    </form>
  </div>
</div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const showModal = ref(false)
const inputMethod = ref('project') // Default to project selection
const citations = ref([
  {
    title: 'Research Paper Title',
    authors: 'John Doe, Jane Smith (2023)',
  },
  {
    title: 'Research Paper Title',
    authors: 'John Doe, Jane Smith (2023)',
  },
  {
    title: 'Research Paper Title',
    authors: 'John Doe, Jane Smith (2023)',
  }
])

const formats = ['APA', 'MLA', 'Chicago', 'Harvard']

const projects = ref([
  { id: 1, name: 'Project Alpha' },
  { id: 2, name: 'Project Beta' },
  { id: 3, name: 'Project Gamma' },
])

const newCitation = ref({
  project: '',
  text: '',
})

const isFormValid = computed(() => {
  if (inputMethod.value === 'project') {
    return !!newCitation.value.project
  }
  return !!newCitation.value.text.trim()
})

const addCitation = () => {
  if (!isFormValid.value) return

  citations.value.push({
    title: inputMethod.value === 'project' 
      ? `Project Citation: ${projects.value.find(p => p.id === newCitation.value.project)?.name || 'Untitled'}`
      : newCitation.value.text.substring(0, 30) + '...',
    authors: 'Pending Author Info',
  })
  
  newCitation.value = { project: '', text: '' }
  inputMethod.value = 'project'
  showModal.value = false
}
</script>