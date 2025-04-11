<template>
    <main class="flex-1 overflow-auto bg-gray-100 p-6">
      <div class="max-w-3xl mx-auto">
        <div class="flex justify-between items-center mb-6">
          <h2 class="text-2xl font-semibold text-gray-800">Research Hub</h2>
          <!-- <NuxtLink to="/create-post" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm">
            Create Post
          </NuxtLink> -->
        </div>
        <div class="mb-6 bg-white p-4 rounded-lg shadow-sm">
          <textarea
            v-model="newPost"
            placeholder="Share your research updates..."
            class="w-full p-3 border border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-300 text-sm"
            rows="3"
          ></textarea>
          <div class="flex justify-end mt-4">
            <button 
              class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm"
              :disabled="!newPost.trim()"
              @click="postUpdate"
            >
              Post Research
            </button>
          </div>
        </div>
        <div class="space-y-4">
          <div v-for="(post, index) in posts" :key="index" class="bg-white p-4 rounded-lg shadow-sm">
            <div class="flex items-start space-x-4">
              <img :src="post.avatar" :alt="post.author" class="w-12 h-12 rounded-full">
              <div class="flex-1">
                <div class="flex items-center justify-between">
                  <div>
                    <h3 class="font-semibold text-gray-800">{{ post.author }}</h3>
                    <p class="text-sm text-gray-500">{{ post.group }} • {{ post.time }}</p>
                  </div>
                  <button class="text-blue-600 hover:text-blue-700">
                    <i class="fas fa-user-plus w-5 h-5"></i>
                  </button>
                </div>
                <p class="mt-3 text-gray-700">{{ post.content }}</p>
                <div class="mt-4 flex items-center space-x-4">
                  <button class="flex items-center text-gray-600 hover:text-blue-600">
                    <i class="fas fa-heart w-5 h-5 mr-1"></i>
                    {{ post.likes }}
                  </button>
                  <button class="flex items-center text-gray-600 hover:text-blue-600">
                    <i class="fas fa-comment w-5 h-5 mr-1"></i>
                    {{ post.comments }}
                  </button>
                  <button class="flex items-center text-gray-600 hover:text-blue-600">
                    <i class="fas fa-share w-5 h-5 mr-1"></i>
                    Share
                  </button>
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
  
  const newPost = ref('')
  const posts = ref([
    {
      author: 'Dr. Sarah Johnson',
      avatar: 'https://randomuser.me/api/portraits/women/1.jpg',
      group: 'AI Research Group',
      time: '2 hours ago',
      content: 'Just published our latest findings on neural network optimization techniques. Looking for feedback from the community!',
      likes: 24,
      comments: 8,
    },
    {
      author: 'Prof. Michael Chen',
      avatar: 'https://randomuser.me/api/portraits/men/1.jpg',
      group: 'Database Systems',
      time: '5 hours ago',
      content: 'Exciting breakthrough in distributed database performance optimization. Full paper coming soon!',
      likes: 45,
      comments: 12,
    },
])
  
const postUpdate = () => {
    if (newPost.value.trim()) {
      posts.value.unshift({
        author: 'Current User', // Replace with actual user data
        avatar: 'https://randomuser.me/api/portraits/women/2.jpg', // Replace with actual user avatar
        group: 'Your Research Group', // Replace with actual group
        time: 'Just now',
        content: newPost.value,
        likes: 0,
        comments: 0,
      })
      newPost.value = ''
    }
  }
</script>