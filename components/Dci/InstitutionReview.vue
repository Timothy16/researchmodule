<template>
    <div class="p-6">
      <h2 class="text-xl font-semibold text-gray-800 mb-6">Institutional Review</h2>
      
      <!-- Approval Workflow -->
      <div class="mb-8">
        <div class="border border-gray-200 rounded-md p-4 bg-white">
          <h3 class="text-lg font-medium text-gray-900">Approval Workflow</h3>
          <div class="mt-4">
            <DciApprovalWorkflow current-view="institution-review" />
          </div>
        </div>
      </div>
      
      <!-- Reviewer Information -->
      <div class="bg-white shadow overflow-hidden sm:rounded-lg mb-8">
        <div class="px-4 py-5 sm:px-6">
          <h3 class="text-lg leading-6 font-medium text-gray-900">Reviewer Information</h3>
        </div>
        <div class="border-t border-gray-200 px-4 py-5 sm:p-6">
          <dl class="grid grid-cols-1 gap-x-4 gap-y-6 sm:grid-cols-2">
            <div class="sm:col-span-1">
              <dt class="text-sm font-medium text-gray-500 flex items-center">
                <i class="fas fa-user w-4 h-4 mr-2"></i>Assigned Reviewer
              </dt>
              <dd class="mt-1 text-sm text-gray-900">Dr. Sarah Johnson</dd>
            </div>
            <div class="sm:col-span-1">
              <dt class="text-sm font-medium text-gray-500 flex items-center">
                <i class="fas fa-calendar w-4 h-4 mr-2"></i>Expected Review Date
              </dt>
              <dd class="mt-1 text-sm text-gray-900">October 15, 2023</dd>
            </div>
            <div class="sm:col-span-2">
              <dt class="text-sm font-medium text-gray-500 flex items-center">
                <i class="fas fa-comment w-4 h-4 mr-2"></i>Initial Assessment
              </dt>
              <dd class="mt-1 text-sm text-gray-900">
                The work appears to meet institutional standards for academic integrity and quality. Proceeding with detailed review.
              </dd>
            </div>
          </dl>
        </div>
      </div>
      
      <!-- Activity Log -->
      <div class="bg-white shadow overflow-hidden sm:rounded-lg mb-8">
        <div class="px-4 py-5 sm:px-6">
          <h3 class="text-lg leading-6 font-medium text-gray-900">Activity Log</h3>
        </div>
        <div class="border-t border-gray-200">
          <ul class="divide-y divide-gray-200">
            <li v-for="(activity, index) in activityLog" :key="index" class="px-4 py-4 sm:px-6">
              <div class="flex items-center justify-between">
                <p class="text-sm font-medium text-blue-600 truncate">{{ activity.title }}</p>
                <div class="ml-2 flex-shrink-0 flex">
                  <p :class="getStatusClass(activity.status)">{{ activity.status }}</p>
                </div>
              </div>
              <div class="mt-2 flex justify-between">
                <div class="sm:flex">
                  <p class="flex items-center text-sm text-gray-500">
                    <i class="fas fa-user flex-shrink-0 mr-1.5 h-4 w-4 text-gray-400"></i>
                    {{ activity.performer }}
                  </p>
                </div>
                <p class="mt-2 flex items-center text-sm text-gray-500 sm:mt-0">
                  <i class="fas fa-calendar flex-shrink-0 mr-1.5 h-4 w-4 text-gray-400"></i>
                  {{ activity.date }}
                </p>
              </div>
            </li>
          </ul>
        </div>
      </div>
      
      <!-- Comments & Feedback -->
      <div class="bg-white shadow overflow-hidden sm:rounded-lg mb-8">
        <div class="px-4 py-5 sm:px-6">
          <h3 class="text-lg leading-6 font-medium text-gray-900">Comments &amp; Feedback</h3>
        </div>
        <div class="border-t border-gray-200 px-4 py-5 sm:p-6">
          <div class="space-y-4">
            <div v-for="(comment, index) in comments" :key="index" :class="`bg-${comment.type}-50 p-4 rounded-md`">
              <div class="flex">
                <div class="flex-shrink-0">
                  <i :class="`fas fa-user h-5 w-5 text-${comment.type}-400`"></i>
                </div>
                <div class="ml-3">
                  <h3 :class="`text-sm font-medium text-${comment.type}-800`">{{ comment.author }}</h3>
                  <div :class="`mt-2 text-sm text-${comment.type}-700`">
                    <p>{{ comment.text }}</p>
                  </div>
                  <div :class="`mt-2 text-xs text-${comment.type}-500`">
                    <p>{{ comment.date }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="mt-6">
            <label for="comment" class="block text-sm font-medium text-gray-700">Add your comment</label>
            <div class="mt-1">
              <textarea
                rows="3"
                name="comment"
                id="comment"
                class="shadow-sm focus:ring-blue-500 focus:border-blue-500 block w-full sm:text-sm border-gray-300 rounded-md"
                placeholder="Enter your questions or comments for the reviewer"
                v-model="newComment"
              ></textarea>
            </div>
            <div class="mt-2 flex justify-end">
              <button
                type="button"
                class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
                @click="submitComment"
              >
                Submit Comment
              </button>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Navigation Buttons -->
      <div class="mt-8 flex justify-end space-x-4">
        <button 
          type="button" 
          class="inline-flex items-center px-4 py-2 border border-gray-300 shadow-sm text-sm font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
          @click="goToPrevious"
        >
          <i class="fas fa-arrow-left mr-2"></i> Back to Supervisor Review
        </button>
        <button 
          type="button" 
          class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
          @click="goToNext"
        >
          Proceed to DCI Certificate <i class="fas fa-arrow-right ml-2"></i>
        </button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const props = defineProps({
  step: Number
});
const emit = defineEmits(['updateStep']);
  const newComment = ref('');
  
  // Activity log data
  const activityLog = [
    {
      title: 'Review Initiated',
      status: 'Completed',
      performer: 'System',
      date: 'October 10, 2023 - 9:15 AM'
    },
    {
      title: 'Reviewer Assignment',
      status: 'Completed',
      performer: 'Academic Affairs Office',
      date: 'October 10, 2023 - 11:30 AM'
    },
    {
      title: 'Initial Assessment',
      status: 'Completed',
      performer: 'Dr. Sarah Johnson',
      date: 'October 12, 2023 - 2:45 PM'
    },
    {
      title: 'Detailed Review',
      status: 'In Progress',
      performer: 'Dr. Sarah Johnson',
      date: 'October 13, 2023 - 10:20 AM'
    }
  ];
  
  // Comments data
  const comments = [
    {
      author: 'Dr. Sarah Johnson',
      text: 'The research methodology is sound and the literature review is comprehensive. The work demonstrates a good understanding of the subject matter.',
      date: 'October 13, 2023 - 10:30 AM',
      type: 'blue'
    },
    {
      author: 'Institution Review System',
      text: 'Automated check: The document complies with institutional formatting guidelines. References match the citation style guide.',
      date: 'October 10, 2023 - 9:20 AM',
      type: 'gray'
    }
  ];
  
  // Get status class based on status text
  const getStatusClass = (status) => {
    const baseClass = 'px-2 inline-flex text-xs leading-5 font-semibold rounded-full';
    if (status === 'Completed') {
      return `${baseClass} bg-green-100 text-green-800`;
    } else if (status === 'In Progress') {
      return `${baseClass} bg-yellow-100 text-yellow-800`;
    } else if (status === 'Pending') {
      return `${baseClass} bg-gray-100 text-gray-800`;
    }
    return baseClass;
  };
  
  const goToNext = () => {
  emit('updateStep', props.step + 1);
  scrollToTop();
};

const goToPrevious = () => {
  emit('updateStep', props.step - 1);
  scrollToTop();
};

const scrollToTop = () => {
  if (typeof window !== 'undefined') {
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }
};
  
  // Submit a new comment
  const submitComment = () => {
    if (newComment.value.trim()) {
      comments.unshift({
        author: 'You',
        text: newComment.value,
        date: new Date().toLocaleString(),
        type: 'blue'
      });
      newComment.value = '';
    } else {
      alert('Please enter a comment before submitting.');
    }
  };
  </script>