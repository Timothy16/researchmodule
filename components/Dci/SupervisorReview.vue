<template>
    <div class="p-6">
      <h2 class="text-xl font-semibold text-gray-800 mb-6">Supervisor Review</h2>
      
      <!-- Approval Workflow -->
      <div class="mb-8">
        <div class="border border-gray-200 rounded-md p-4 bg-white">
          <h3 class="text-lg font-medium text-gray-900">Approval Workflow</h3>
          <div class="mt-4">
            <DciApprovalWorkflow current-view="supervisor-review" />
          </div>
        </div>
      </div>
      
      <!-- Supervisor Information -->
      <div class="bg-white shadow overflow-hidden sm:rounded-lg mb-8">
        <div class="px-4 py-5 sm:px-6">
          <h3 class="text-lg leading-6 font-medium text-gray-900">Supervisor Information</h3>
        </div>
        <div class="border-t border-gray-200 px-4 py-5 sm:p-6">
          <dl class="grid grid-cols-1 gap-x-4 gap-y-6 sm:grid-cols-2">
            <div class="sm:col-span-1">
              <dt class="text-sm font-medium text-gray-500">Supervisor Name</dt>
              <dd class="mt-1 text-sm text-gray-900">Prof. Michael Thompson</dd>
            </div>
            <div class="sm:col-span-1">
              <dt class="text-sm font-medium text-gray-500">Department</dt>
              <dd class="mt-1 text-sm text-gray-900">Computer Science</dd>
            </div>
            <div class="sm:col-span-1">
              <dt class="text-sm font-medium text-gray-500">Email</dt>
              <dd class="mt-1 text-sm text-gray-900">m.thompson@university.edu</dd>
            </div>
            <div class="sm:col-span-1">
              <dt class="text-sm font-medium text-gray-500">Status</dt>
              <dd class="mt-1 text-sm text-gray-900">
                <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-yellow-100 text-yellow-800">Review Pending</span>
              </dd>
            </div>
          </dl>
        </div>
      </div>
      
      <!-- Supervisor Feedback -->
      <div class="bg-white shadow overflow-hidden sm:rounded-lg mb-8">
        <div class="px-4 py-5 sm:px-6">
          <h3 class="text-lg leading-6 font-medium text-gray-900">Supervisor Feedback</h3>
        </div>
        <div class="border-t border-gray-200 px-4 py-5 sm:p-6">
          <div class="space-y-4">
            <div class="bg-gray-50 p-4 rounded-md">
              <div class="flex">
                <div class="flex-shrink-0">
                  <i class="fas fa-comment h-5 w-5 text-gray-400"></i>
                </div>
                <div class="ml-3">
                  <h3 class="text-sm font-medium text-gray-800">System Notification</h3>
                  <div class="mt-2 text-sm text-gray-700">
                    <p>Supervisor has been notified about the pending review on October 13, 2023. Typical response time is 3-5 business days.</p>
                  </div>
                  <div class="mt-2 text-xs text-gray-500">
                    <p>October 13, 2023 - 3:45 PM</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="mt-6 border-t border-gray-200 pt-6">
            <h4 class="text-sm font-medium text-gray-900">Previous Feedback History</h4>
            <div class="mt-4 space-y-4">
              <div class="bg-blue-50 p-4 rounded-md">
                <div class="flex">
                  <div class="flex-shrink-0">
                    <i class="fas fa-user h-5 w-5 text-blue-400"></i>
                  </div>
                  <div class="ml-3">
                    <h3 class="text-sm font-medium text-blue-800">Prof. Michael Thompson</h3>
                    <div class="mt-2 text-sm text-blue-700">
                      <p>Initial research proposal was well-structured. Please ensure you address the methodology concerns we discussed in your final submission.</p>
                    </div>
                    <div class="mt-2 text-xs text-blue-500">
                      <p>September 15, 2023 - 10:30 AM</p>
                    </div>
                  </div>
                </div>
              </div>
              <div class="bg-blue-50 p-4 rounded-md">
                <div class="flex">
                  <div class="flex-shrink-0">
                    <i class="fas fa-user h-5 w-5 text-blue-400"></i>
                  </div>
                  <div class="ml-3">
                    <h3 class="text-sm font-medium text-blue-800">Prof. Michael Thompson</h3>
                    <div class="mt-2 text-sm text-blue-700">
                      <p>Progress report shows good development. Your literature review is thorough. Focus on strengthening your analysis section in the final draft.</p>
                    </div>
                    <div class="mt-2 text-xs text-blue-500">
                      <p>August 22, 2023 - 2:15 PM</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Supervisor Decision Options -->
      <div class="bg-white shadow overflow-hidden sm:rounded-lg mb-8">
        <div class="px-4 py-5 sm:px-6">
          <h3 class="text-lg leading-6 font-medium text-gray-900">Supervisor Decision Options</h3>
          <p class="mt-1 max-w-2xl text-sm text-gray-500">These options will be available to your supervisor when reviewing your work.</p>
        </div>
        <div class="border-t border-gray-200">
          <div class="px-4 py-5 sm:p-6">
            <div class="space-y-4">
              <div class="flex items-start">
                <div class="flex-shrink-0">
                  <i class="fas fa-square-check h-5 w-5 text-green-500"></i>
                </div>
                <div class="ml-3">
                  <h3 class="text-sm font-medium text-gray-900">Approve</h3>
                  <p class="text-sm text-gray-500">Approve the work as meeting all academic standards and ready for DCI issuance.</p>
                </div>
              </div>
              <div class="flex items-start">
                <div class="flex-shrink-0">
                  <i class="fas fa-square-xmark h-5 w-5 text-yellow-500"></i>
                </div>
                <div class="ml-3">
                  <h3 class="text-sm font-medium text-gray-900">Request Revisions</h3>
                  <p class="text-sm text-gray-500">Request specific revisions before the work can be approved for DCI issuance.</p>
                </div>
              </div>
              <div class="flex items-start">
                <div class="flex-shrink-0">
                  <i class="fas fa-square-xmark h-5 w-5 text-red-500"></i>
                </div>
                <div class="ml-3">
                  <h3 class="text-sm font-medium text-gray-900">Reject</h3>
                  <p class="text-sm text-gray-500">Reject the work as not meeting academic standards required for DCI issuance.</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Send Message to Supervisor -->
      <div class="bg-white shadow overflow-hidden sm:rounded-lg mb-8">
        <div class="px-4 py-5 sm:px-6">
          <h3 class="text-lg leading-6 font-medium text-gray-900">Send Message to Supervisor</h3>
        </div>
        <div class="border-t border-gray-200 px-4 py-5 sm:p-6">
          <div>
            <label for="message" class="block text-sm font-medium text-gray-700">Message</label>
            <div class="mt-1">
              <textarea 
                rows="4" 
                name="message" 
                id="message" 
                class="shadow-sm focus:ring-blue-500 focus:border-blue-500 block w-full sm:text-sm border-gray-300 rounded-md" 
                placeholder="Enter any additional information for your supervisor"
                v-model="message"
              ></textarea>
            </div>
          </div>
          <div class="mt-4 flex justify-end">
            <button 
              type="button" 
              class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
              @click="sendMessage"
            >
              Send Message
            </button>
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
          <i class="fas fa-arrow-left mr-2"></i> Back to AI Review
        </button>
        <button 
          type="button" 
          @click="goToNext"
          class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-gray-400 cursor-not-allowed" 
          disabled
        >
          Awaiting Supervisor Approval
        </button>
      </div>
    </div>
</template>
  
  <script setup>
  import { ref } from 'vue';
  

  const message = ref('');
  
  const props = defineProps({
  step: Number
});
const emit = defineEmits(['updateStep']);

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
  
  const sendMessage = () => {
    if (message.value.trim()) {
      alert('Message sent to supervisor: ' + message.value);
      message.value = '';
    } else {
      alert('Please enter a message before sending.');
    }
  };
  </script>