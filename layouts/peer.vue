<template>
  <div class="min-h-screen bg-gray-50 flex">
    <!-- Sidebar Navigation - Full height -->
    <div
      class="bg-white shadow-md w-64 fixed h-screen z-10 transition-all duration-300 overflow-hidden hidden md:block"
    >
      <!-- Logo Area -->
      <div class="p-4 border-b border-gray-200">
        <h2 class="text-xl font-semibold text-gray-800">Menu</h2>
      </div>

      <!-- Navigation Links -->
      <nav class="p-4 flex-1 overflow-y-auto">
        <ul class="space-y-2">
          <li v-for="(item, index) in menuItems" :key="index">
            <NuxtLink
              :to="item.link"
              class="flex items-center p-2 rounded-md transition-colors duration-200"
              :class="
                isActive(item.link)
                  ? 'bg-blue-100 text-blue-600'
                  : 'text-gray-700 hover:bg-blue-50'
              "
            >
              <i :class="item.icon + ' w-6 text-center mr-3'"></i>
              <span>{{ item.label }}</span>
            </NuxtLink>
          </li>
        </ul>
      </nav>
    </div>

    <!-- Mobile sidebar (hidden by default) -->
    <div 
      class="bg-white shadow-md w-full fixed h-auto z-20 transition-all duration-300 overflow-hidden md:hidden"
      :class="{ 'h-0': !mobileMenuOpen, 'h-auto': mobileMenuOpen }"
      style="top: 64px;"
    >
      <nav class="p-4">
        <ul class="space-y-2">
          <li v-for="(item, index) in menuItems" :key="index">
            <NuxtLink
              :to="item.link"
              class="flex items-center p-2 rounded-md transition-colors duration-200"
              :class="
                isActive(item.link)
                  ? 'bg-blue-100 text-blue-600'
                  : 'text-gray-700 hover:bg-blue-50'
              "
              @click="mobileMenuOpen = false"
            >
              <i :class="item.icon + ' w-6 text-center mr-3'"></i>
              <span>{{ item.label }}</span>
            </NuxtLink>
          </li>
        </ul>
      </nav>
    </div>

    <!-- Main Content Area with Top Menu (same column) -->
    <div class="flex-1 md:ml-64 flex flex-col w-full">
      <!-- Top Menu - Now part of the content column -->
      <div class="bg-white shadow p-4 flex items-center justify-between sticky top-0 z-10">
        <div class="flex items-center space-x-2">
          <span class="font-bold text-lg text-gray-800">Academic Peer Review</span>
        </div>
        <button
          @click="toggleMobileMenu"
          class="md:hidden text-gray-600 focus:outline-none"
        >
          <i class="fas fa-bars"></i>
        </button>
      </div>

      <!-- Content -->
      <div class="p-4 md:p-8 flex-1">
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
  { label: 'Home', icon: 'fas fa-home', link: '/' },
  { label: 'Submit Paper', icon: 'fas fa-file-upload', link: '/peer-review/submit' },
  { label: 'Reviewers', icon: 'fas fa-users', link: '/peer-review/reviewers' },
  { label: 'Reviews', icon: 'fas fa-file-alt', link: '/peer-review/reviews' },
]
</script>

<style scoped>
/* Active link styling for NuxtLink */
.nuxt-link-exact-active {
  @apply bg-blue-100 text-blue-600;
}
</style>