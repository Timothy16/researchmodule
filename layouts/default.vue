<template>
    <div class="min-h-screen bg-gray-50 flex flex-col md:flex-row">
      <!-- Mobile Header with Menu Toggle -->
      <div class="md:hidden bg-white shadow p-4 flex items-center justify-between sticky top-0 z-20">
        <div class="flex items-center space-x-2">
          <span class="font-bold text-lg text-gray-800">Research Module</span>
        </div>
        <button @click="toggleMobileMenu" class="text-gray-600 focus:outline-none">
          <i class="fas fa-bars"></i>
        </button>
      </div>
  
      <!-- Sidebar Navigation -->
      <div class="bg-white shadow-md w-full md:w-64 transition-all duration-300 overflow-hidden md:fixed md:h-screen z-10"
           :class="{'h-0': !mobileMenuOpen, 'h-auto': mobileMenuOpen}">
        <!-- Desktop Logo Area -->
        <div class="p-4 border-b border-gray-200">
          <h2 class="text-xl font-semibold text-gray-800">Research Module</h2>
        </div>
        
        <!-- Navigation Links -->
        <nav class="p-4 flex-1 overflow-y-auto">
          <ul class="space-y-2">
            <li v-for="(item, index) in menuItems" :key="index">
              <NuxtLink 
                :to="item.link"
                class="flex items-center p-2 rounded-md transition-colors duration-200"
                :class="isActive(item.link) ? 'bg-blue-100 text-blue-600' : 'text-gray-700 hover:bg-blue-50'"
                @click="mobileMenuOpen = false"
              >
                <i :class="item.icon + ' w-6 text-center mr-3'"></i>
                <span>{{ item.label }}</span>
              </NuxtLink>
            </li>
          </ul>
        </nav>
      </div>
  
      <!-- Main Content Area -->
      <div class="flex-1 md:ml-64 w-full transition-all duration-300">
        <div class="p-4 md:p-8">
          <slot />
        </div>
      </div>
    </div>
</template>
  
<script setup>
  import { ref } from 'vue'
  import { useRoute } from 'vue-router'
  
  // Mobile menu state
  const mobileMenuOpen = ref(false)
  const toggleMobileMenu = () => {
    mobileMenuOpen.value = !mobileMenuOpen.value
  }
  
  // Get current route
  const route = useRoute()
  
  // Function to check if route is active
  const isActive = (link) => {
    return route.path === link
  }
  
  // Menu items with links
  const menuItems = [
    { label: 'Projects', icon: 'fas fa-folder-open', link: '/' },
    { label: 'Research Hub', icon: 'fas fa-users', link: '/research-hub' },
    { label: 'Peer Review', icon: 'fas fa-file-alt', link: '/peer-review' },
    { label: 'Research Assistant', icon: 'fas fa-robot', link: '/research-assistant' },
    { label: 'Repository', icon: 'fas fa-archive', link: '/repository' },
    
    { label: 'Ethics & Compliance', icon: 'fas fa-balance-scale', link: '/ethics-compliance' },
    { label: 'Grants & Funding', icon: 'fas fa-hand-holding-usd', link: '/grants-funding' },
    { label: 'Data', icon: 'fas fa-chart-bar', link: '/data' },
    { label: 'Citations', icon: 'fas fa-book', link: '/citations' },
    { label: 'Conferences', icon: 'fas fa-users', link: '/conferences' },
    { label: 'Discussions', icon: 'fas fa-comments', link: '/discussions' },
  ]
  </script>
  
<style scoped>
  /* Fixed sidebar styling */
  @media (min-width: 768px) {
    .md\:ml-64 {
      margin-left: 16rem;
    }
    
    .md\:fixed {
      position: fixed;
    }
    
    .md\:h-screen {
      height: 100vh;
    }
  }
  
  /* Active link styling for NuxtLink */
  .nuxt-link-exact-active {
    @apply bg-blue-100 text-blue-600;
  }
 </style>