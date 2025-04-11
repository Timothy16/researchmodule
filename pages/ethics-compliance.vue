<template>
    <main class="flex-1 overflow-auto bg-gray-100">
      <div class="p-6">
        <h2 class="text-2xl font-semibold mb-6 text-gray-800">Ethics & Compliance</h2>
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
          <!-- Main Content -->
          <div class="lg:col-span-2 space-y-4">
            <!-- Compliance Checker -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
                <h3 class="text-lg font-semibold mb-4 text-gray-800">Compliance Checker</h3>
                <div class="space-y-4">
                    <div>
                    <label for="project" class="block text-sm font-medium text-gray-700 mb-2">Select Project</label>
                    <select 
                        v-model="selectedProject"
                        id="project"
                        class="w-full border border-gray-200 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-blue-300 text-sm"
                    >
                        <option value="">Select a project</option>
                        <option v-for="project in projects" :key="project.id" :value="project.id">
                        {{ project.name }}
                        </option>
                    </select>
                    </div>
                    <button 
                    class="w-full py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm"
                    :disabled="!selectedProject"
                    >
                    Check Compliance
                    </button>
                </div>
            </div>
  
            <!-- Active Applications -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
              <h3 class="text-lg font-semibold mb-4 text-gray-800">Active Applications</h3>
              <div v-for="(application, index) in activeApplications" :key="index" class="mb-4 p-4 border border-gray-200 rounded-lg">
                <div class="flex items-start justify-between">
                  <div>
                    <h4 class="font-medium text-gray-800 mb-2">{{ application.title }}</h4>
                    <p class="text-sm text-gray-500 mb-2">Submitted: {{ application.submitted }}</p>
                    <div class="flex items-center space-x-2">
                      <span class="px-2 py-1 text-xs bg-blue-100 text-blue-700 rounded">
                        {{ application.status }}
                      </span>
                    </div>
                  </div>
                  <button class="text-blue-600 hover:text-blue-700 text-sm font-medium">
                    View Details
                  </button>
                </div>
              </div>
            </div>
          </div>
  
          <!-- Sidebar -->
          <div class="space-y-4">
            <!-- Compliance Status -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
              <h3 class="text-lg font-semibold mb-4 text-gray-800">Compliance Status</h3>
              <div class="space-y-3">
                <div v-for="(status, index) in complianceStatus" :key="index" :class="status.bgColor" class="flex items-center justify-between p-3 rounded-lg">
                  <div class="flex items-center space-x-3">
                    <i :class="[status.icon, 'w-5', 'h-5', status.iconColor]"></i>
                    <span class="text-gray-800">{{ status.title }}</span>
                  </div>
                  <span :class="status.textColor" class="font-medium">{{ status.status }}</span>
                </div>
              </div>
            </div>
  
            <!-- Required Documents -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
              <h3 class="text-lg font-semibold mb-4 text-gray-800">Required Documents</h3>
              <div class="space-y-3">
                <div v-for="(document, index) in requiredDocuments" :key="index" class="flex items-start space-x-3">
                  <i class="fas fa-clipboard-list w-5 h-5 text-gray-400"></i>
                  <div>
                    <p class="font-medium text-gray-800">{{ document.title }}</p>
                    <p class="text-sm text-gray-500">Last updated: {{ document.lastUpdated }}</p>
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
  
  const selectedProject = ref('')
const projects = ref([
  { id: 1, name: 'Project Alpha' },
  { id: 2, name: 'Project Beta' },
  { id: 3, name: 'Project Gamma' },
])

  const activeApplications = ref([
    {
      title: 'Human Subject Research - Phase 1',
      submitted: 'Jan 15, 2024',
      status: 'Under Review',
    },
    {
      title: 'Human Subject Research - Phase 1',
      submitted: 'Jan 15, 2024',
      status: 'Under Review',
    },
  ])
  
  const complianceStatus = ref([
    {
      title: 'IRB Training',
      status: 'Complete',
      icon: 'fas fa-check-circle',
      iconColor: 'text-green-600',
      bgColor: 'bg-green-50',
      textColor: 'text-green-600',
    },
    {
      title: 'Data Management Plan',
      status: 'Pending',
      icon: 'fas fa-exclamation-circle',
      iconColor: 'text-yellow-600',
      bgColor: 'bg-yellow-50',
      textColor: 'text-yellow-600',
    },
    {
      title: 'Ethics Certificate',
      status: 'Valid',
      icon: 'fas fa-shield-alt',
      iconColor: 'text-green-600',
      bgColor: 'bg-green-50',
      textColor: 'text-green-600',
    },
  ])
  
  const requiredDocuments = ref([
    { title: 'Consent Form Template', lastUpdated: '1 month ago' },
    { title: 'Ethics Review Checklist', lastUpdated: '2 weeks ago' },
    { title: 'Data Privacy Agreement', lastUpdated: '3 days ago' },
  ])
  </script>