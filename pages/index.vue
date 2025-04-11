<template>
    <div class="flex-1 overflow-auto bg-gray-100">
      <main class=" p-6">
        <div class="">
          <!-- Header with Create Button -->
          <div class="flex justify-between items-center mb-6">
            <h2 class="text-2xl font-semibold text-gray-800">My Projects</h2>
            <button 
              class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 flex items-center"
              @click="showModal = true"
            >
              <i class="fas fa-plus mr-2"></i>
              Create New Project
            </button>
          </div>
  
          <!-- Project Cards Grid -->
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            <!-- Project Card (v-for loop) -->
            <div 
              v-for="project in projects" 
              :key="project.id" 
              class="bg-white p-6 rounded-lg border border-gray-200 shadow-sm hover:shadow-md transition-shadow"
            >
              <h3 class="text-lg font-semibold text-gray-800 mb-2">{{ project.title }}</h3>
              <p class="text-gray-600 mb-4">{{ project.description }}</p>
              <div class="border-t border-gray-100 pt-4">
                <h4 class="text-sm font-medium text-gray-700 mb-2">Team Members</h4>
                <div class="flex flex-wrap gap-2">
                  <div 
                    v-for="member in project.members" 
                    :key="member.id"
                    class="flex items-center bg-blue-50 text-blue-700 px-3 py-1 rounded-full text-sm"
                  >
                    <i class="fas fa-user-circle mr-1"></i>
                    {{ member.name }}
                  </div>
                </div>
              </div>
            </div>
  
            <!-- Empty State -->
            <div 
              v-if="projects.length === 0" 
              class="col-span-full flex flex-col items-center justify-center p-12 bg-white rounded-lg border border-dashed border-gray-300"
            >
              <i class="fas fa-folder-open text-gray-400 text-4xl mb-4"></i>
              <h3 class="text-lg font-medium text-gray-700 mb-2">No projects yet</h3>
              <p class="text-gray-500 text-center mb-4">Create your first project to get started</p>
              <button 
                @click="showModal = true"
                class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700"
              >
                Create Project
              </button>
            </div>
          </div>
        </div>
      </main>
  
      <!-- Create Project Modal -->
      <div 
        v-if="showModal" 
        class="fixed inset-0 bg-gray-600 bg-opacity-50 flex items-center justify-center z-50"
      >
        <div class="bg-white rounded-lg shadow-xl w-full max-w-md">
          <div class="flex justify-between items-center p-6 border-b border-gray-200">
            <h3 class="text-lg font-semibold text-gray-800">Create New Project</h3>
            <button @click="showModal = false" class="text-gray-400 hover:text-gray-600">
              <i class="fas fa-times"></i>
            </button>
          </div>
          
          <form @submit.prevent="createProject" class="p-6">
            <div class="space-y-4">
              <!-- Project Title -->
              <div>
                <label for="title" class="block text-sm font-medium text-gray-700 mb-1">Project Title</label>
                <input 
                  id="title"
                  v-model="newProject.title"
                  type="text" 
                  class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                  placeholder="Enter project title"
                  required
                >
              </div>
              
              <!-- Project Description -->
              <div>
                <label for="description" class="block text-sm font-medium text-gray-700 mb-1">Description</label>
                <textarea 
                  id="description"
                  v-model="newProject.description"
                  class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                  rows="3"
                  placeholder="Enter project description"
                  required
                ></textarea>
              </div>
              
              <!-- Invite Members -->
              <div>
                <label for="emails" class="block text-sm font-medium text-gray-700 mb-1">Invite Team Members</label>
                <div class="flex items-center">
                  <input 
                    id="emails"
                    v-model="newMemberEmail"
                    type="email" 
                    class="flex-1 px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                    placeholder="Enter email address"
                    @keydown.enter.prevent="addMember"
                  >
                  <button 
                    type="button"
                    @click="addMember"
                    class="ml-2 px-3 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700"
                  >
                    <i class="fas fa-plus"></i>
                  </button>
                </div>
                <p class="text-xs text-gray-500 mt-1">Press Enter or click + to add multiple emails</p>
                
                <!-- Email Tags -->
                <div v-if="newProject.invitedEmails.length > 0" class="flex flex-wrap gap-2 mt-3">
                  <div 
                    v-for="(email, index) in newProject.invitedEmails" 
                    :key="index"
                    class="bg-blue-50 text-blue-800 px-3 py-1 rounded-full flex items-center text-sm"
                  >
                    {{ email }}
                    <button 
                      type="button"
                      @click="removeMember(index)" 
                      class="ml-1 text-blue-500 hover:text-blue-700"
                    >
                      <i class="fas fa-times-circle"></i>
                    </button>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="flex justify-end mt-6 space-x-3">
              <button 
                type="button"
                @click="showModal = false"
                class="px-4 py-2 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50"
              >
                Cancel
              </button>
              <button 
                type="submit"
                class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700"
              >
                Create Project
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
</template>
  
  <script setup>
  import { ref, reactive } from 'vue'
  
  // Modal state
  const showModal = ref(false)
  
  // Project form data
  const newProject = reactive({
    title: '',
    description: '',
    invitedEmails: []
  })
  
  // Email input for adding members
  const newMemberEmail = ref('')
  
  // Sample projects data (would normally come from API)
  const projects = ref([
    {
      id: 1,
      title: 'Neural Network Research',
      description: 'Exploring advanced neural network architectures for image recognition in medical diagnostics.',
      members: [
        { id: 1, name: 'Sarah Johnson' },
        { id: 2, name: 'Michael Chen' },
        { id: 3, name: 'David Wilson' }
      ]
    },
    {
      id: 2,
      title: 'Blockchain Implementation',
      description: 'Developing a secure blockchain system for academic credential verification.',
      members: [
        { id: 4, name: 'Emily Taylor' },
        { id: 5, name: 'James Rodriguez' }
      ]
    },
    {
      id: 3,
      title: 'Climate Data Analysis',
      description: 'Analyzing climate datasets to identify patterns and predict future trends.',
      members: [
        { id: 6, name: 'Robert Brown' },
        { id: 7, name: 'Lisa Chen' },
        { id: 8, name: 'Thomas Wright' }
      ]
    },
    {
      id: 4,
      title: 'Climate Data Analysis',
      description: 'Analyzing climate datasets to identify patterns and predict future trends.',
      members: [
        { id: 6, name: 'Robert Brown' },
        { id: 7, name: 'Lisa Chen' },
        { id: 8, name: 'Thomas Wright' }
      ]
    },
    
    {
      id: 5,
      title: 'Neural Network Research',
      description: 'Exploring advanced neural network architectures for image recognition in medical diagnostics.',
      members: [
        { id: 1, name: 'Sarah Johnson' },
        { id: 2, name: 'Michael Chen' },
        { id: 3, name: 'David Wilson' }
      ]
    },
    {
      id: 6,
      title: 'Blockchain Implementation',
      description: 'Developing a secure blockchain system for academic credential verification.',
      members: [
        { id: 4, name: 'Emily Taylor' },
        { id: 5, name: 'James Rodriguez' }
      ]
    },
  ])
  
  // Add a member email to the invite list
  function addMember() {
    if (newMemberEmail.value && !newProject.invitedEmails.includes(newMemberEmail.value)) {
      newProject.invitedEmails.push(newMemberEmail.value)
      newMemberEmail.value = ''
    }
  }
  
  // Remove a member email from the invite list
  function removeMember(index) {
    newProject.invitedEmails.splice(index, 1)
  }
  
  // Create a new project
  function createProject() {
    // Create new project object
    const project = {
      id: Date.now(), // Simple temporary ID
      title: newProject.title,
      description: newProject.description,
      members: newProject.invitedEmails.map((email, index) => ({
        id: Date.now() + index,
        name: email.split('@')[0] // Using part of email as temporary name
      }))
    }
    
    // Add to projects array
    projects.value.push(project)
    
    // Reset form
    newProject.title = ''
    newProject.description = ''
    newProject.invitedEmails = []
    
    // Close modal
    showModal.value = false
  }
  </script>