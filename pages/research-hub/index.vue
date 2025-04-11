<template>
  <main class="flex-1 overflow-auto bg-gray-100">
    <div class="p-6">
      <div class="flex justify-between items-center mb-6">
        <h2 class="text-2xl font-semibold text-gray-800">Research Hub</h2>
        <button
          @click="openModal"
          class="flex items-center space-x-2 px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm"
        >
          <i class="fas fa-user-plus w-5 h-5"></i>
          <span>Create Research Group</span>
        </button>
      </div>
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <!-- Active Research Groups -->
        <div class="col-span-2">
          <div class="bg-white rounded-lg p-4 shadow-sm">
            <h3 class="text-lg font-semibold mb-4 text-gray-800">Active Research Groups</h3>
            <div class="space-y-4">
              <NuxtLink
                v-for="(group, index) in researchGroups"
                :key="index"
                to="/research-hub/hub"
                class="flex items-center justify-between p-4 rounded-lg shadow-sm hover:bg-gray-50"
              >
                <div class="flex items-center space-x-4">
                  <div class="p-2 bg-blue-50 rounded-full">
                    <i class="fas fa-users w-6 h-6 text-blue-600"></i>
                  </div>
                  <div>
                    <h4 class="font-medium text-gray-800">{{ group.name }}</h4>
                    <p class="text-sm text-gray-500">{{ group.members }} members • Last active {{ group.lastActive }}</p>
                  </div>
                </div>
                <button class="text-blue-600 hover:text-blue-700 text-sm font-medium">Join Group</button>
              </NuxtLink>
            </div>
          </div>
        </div>

        <!-- Sidebar -->
        <div class="space-y-4">
          <!-- Recent Discussions -->
          <div class="bg-white rounded-lg p-4 shadow-sm">
            <h3 class="text-lg font-semibold mb-4 text-gray-800">Recent Discussions</h3>
            <div class="space-y-3">
              <div v-for="(discussion, index) in recentDiscussions" :key="index" class="flex items-start space-x-3">
                <i class="fas fa-comment w-5 h-5 text-gray-400"></i>
                <div>
                  <p class="font-medium text-gray-800">{{ discussion.title }}</p>
                  <p class="text-sm text-gray-500">Posted {{ discussion.posted }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal -->
    <div
      v-if="isModalOpen"
      class="fixed inset-0 bg-gray-600 bg-opacity-50 flex items-center justify-center z-50"
      @click.self="closeModal"
    >
      <div class="bg-white rounded-lg p-6 w-full max-w-md">
        <h3 class="text-lg font-semibold mb-4 text-gray-800">Create Research Group</h3>
        <form @submit.prevent="createGroup">
          <div class="mb-4">
            <label for="groupTitle" class="block text-sm font-medium text-gray-700">Group Title</label>
            <input
              v-model="groupTitle"
              type="text"
              id="groupTitle"
              class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
              placeholder="Enter group title"
              required
            />
          </div>
          <div class="mb-4">
            <label for="emailInvites" class="block text-sm font-medium text-gray-700">Invite Members (Emails)</label>
            <div v-for="(email, index) in emailInvites" :key="index" class="flex items-center space-x-2 mb-2">
              <input
                v-model="emailInvites[index]"
                type="email"
                class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                placeholder="Enter email"
              />
              <button
                type="button"
                @click="removeEmail(index)"
                class="text-red-600 hover:text-red-800"
                v-if="emailInvites.length > 1"
              >
                <i class="fas fa-trash w-5 h-5"></i>
              </button>
            </div>
            <button
              type="button"
              @click="addEmailField"
              class="text-blue-600 hover:text-blue-800 text-sm font-medium"
            >
              + Add another email
            </button>
          </div>
          <div class="flex justify-end space-x-3">
            <button
              type="button"
              @click="closeModal"
              class="px-4 py-2 bg-gray-200 text-gray-800 rounded-lg hover:bg-gray-300"
            >
              Cancel
            </button>
            <button
              type="submit"
              class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700"
            >
              Create Group
            </button>
          </div>
        </form>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from 'vue'

const researchGroups = ref([
  {
    name: 'AI Ethics Research Group',
    members: 8,
    lastActive: '2h ago',
  },
  {
    name: 'Machine Learning Innovators',
    members: 12,
    lastActive: '5h ago',
  },
  {
    name: 'Data Science Collective',
    members: 10,
    lastActive: '1d ago',
  },
])

const recentDiscussions = ref([
  { title: 'Research Methodology Question', posted: '1h ago' },
  { title: 'Best Practices for Data Collection', posted: '3h ago' },
  { title: 'Ethics in AI Research', posted: '5h ago' },
])

// Modal state
const isModalOpen = ref(false)
const groupTitle = ref('')
const emailInvites = ref(['']) // Initialize with one empty email field

// Modal methods
const openModal = () => {
  isModalOpen.value = true
}

const closeModal = () => {
  isModalOpen.value = false
  resetForm()
}

const addEmailField = () => {
  emailInvites.value.push('')
}

const removeEmail = (index) => {
  emailInvites.value.splice(index, 1)
}

const resetForm = () => {
  groupTitle.value = ''
  emailInvites.value = ['']
}

const createGroup = () => {
  // Filter out empty emails and validate
  const validEmails = emailInvites.value.filter(email => email.trim() !== '')
  if (!groupTitle.value.trim()) {
    alert('Group title is required')
    return
  }

  // Simulate adding the group to researchGroups
  researchGroups.value.push({
    name: groupTitle.value,
    members: validEmails.length + 1, // Include creator
    lastActive: 'Now',
  })

  console.log('Group created:', {
    title: groupTitle.value,
    invitedEmails: validEmails,
  })

  // Reset and close modal
  closeModal()
}
</script>