<template>
  <main class="flex-1 overflow-auto p-6">
    <div class="max-w-4xl mx-auto">
      <h2 class="text-2xl font-semibold text-gray-800 mb-6">Welcome to Academic Peer Review</h2>
      <p class="text-gray-600 mb-8">
        Start by submitting your research paper for peer review or sign up as a reviewer to help evaluate academic work.
      </p>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <!-- Submit Research Card -->
        <div class="bg-white p-8 rounded-lg border border-gray-200">
          <div class="flex flex-col items-center text-center">
            <div class="w-16 h-16 bg-blue-50 rounded-full flex items-center justify-center mb-4">
              <i class="fas fa-file-upload w-8 h-8 text-blue-600"></i>
            </div>
            <h3 class="text-xl font-semibold mb-4">Submit Research</h3>
            <p class="text-gray-600 mb-6">
              Upload your paper and get valuable feedback from expert peers in your field. Choose from different review modes to suit your needs.
            </p>
            <NuxtLink
              to="/peer-review/submit"
              class="w-full px-6 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors"
            >
              Submit Paper
            </NuxtLink>
          </div>
        </div>
        <!-- Become a Reviewer Card -->
        <div class="bg-white p-8 rounded-lg border border-gray-200">
          <div class="flex flex-col items-center text-center">
            <div class="w-16 h-16 bg-green-50 rounded-full flex items-center justify-center mb-4">
              <i class="fas fa-user-plus w-8 h-8 text-green-600"></i>
            </div>
            <h3 class="text-xl font-semibold mb-4">Become a Reviewer</h3>
            <p class="text-gray-600 mb-6">
              Share your expertise and help advance academic research. Join our community of expert reviewers and earn recognition.
            </p>
            <NuxtLink
              to="/peer-review/reviewers"
              class="w-full px-6 py-3 bg-green-600 text-white rounded-lg hover:bg-green-700 transition-colors"
            >
              Join as Reviewer
            </NuxtLink>
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