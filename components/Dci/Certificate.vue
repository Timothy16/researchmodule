<template>
    <div class="p-6">
      <h2 class="text-xl font-semibold text-gray-800 mb-6">DCI Certificate</h2>
      
      <!-- Approval Workflow -->
      <div class="mb-8">
        <div class="border border-gray-200 rounded-md p-4 bg-white">
          <h3 class="text-lg font-medium text-gray-900">Approval Workflow</h3>
          <div class="mt-4">
            <DciApprovalWorkflow current-view="certificate" />
          </div>
        </div>
      </div>
      
      <!-- Certificate Success Banner -->
      <div class="text-center mb-8">
        <i class="fas fa-check-circle mx-auto h-16 w-16 text-green-500 text-6xl"></i>
        <h3 class="mt-2 text-lg font-medium text-gray-900">Congratulations!</h3>
        <p class="mt-1 text-sm text-gray-500">Your work has been approved and assigned a Digital Content Identifier.</p>
      </div>
      
      <!-- Certificate Card -->
      <div class="bg-white border border-gray-200 rounded-lg shadow-sm overflow-hidden mb-8">
        <!-- Certificate Header -->
        <div class="px-4 py-5 sm:px-6 bg-blue-50 border-b border-gray-200">
          <div class="flex items-center justify-between">
            <h3 class="text-lg leading-6 font-medium text-gray-900">Digital Content Identifier Certificate</h3>
            <div class="flex space-x-2">
              <button type="button" class="inline-flex items-center p-2 border border-gray-300 rounded-md shadow-sm text-sm font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                <i class="fas fa-download h-4 w-4"></i>
              </button>
              <button type="button" class="inline-flex items-center p-2 border border-gray-300 rounded-md shadow-sm text-sm font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                <i class="fas fa-share h-4 w-4"></i>
              </button>
            </div>
          </div>
        </div>
        
        <!-- Certificate Content -->
        <div class="px-4 py-10 sm:px-6 flex flex-col items-center">
          <div class="max-w-3xl w-full">
            <!-- Institution Header -->
            <div class="flex justify-between items-center mb-8">
              <div>
                <h2 class="text-2xl font-bold text-gray-900">University of Technology</h2>
                <p class="text-sm text-gray-500">Department of Computer Science</p>
              </div>
              <div class="h-16 w-16">
                <i class="fas fa-qrcode h-full w-full text-blue-600 text-4xl"></i>
              </div>
            </div>
            
            <!-- DCI Number -->
            <div class="text-center mb-8">
              <h1 class="text-3xl font-bold text-blue-600">Digital Content Identifier</h1>
              <div class="mt-4 space-y-2">
                <p class="text-lg font-medium text-gray-700">DCI: 10.1234/dci.2023.78912</p>
                <div class="flex flex-col items-center space-y-2 text-sm text-gray-500">
                  <p class="font-mono">Machine-readable: https://dci.edu/10.1234/dci.2023.78912</p>
                  <p>Human-readable: https://dci.edu/certificate/10.1234/dci.2023.78912</p>
                  <button type="button" class="inline-flex items-center px-3 py-1 border border-gray-300 shadow-sm text-sm rounded-md text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                    <i class="fas fa-external-link h-4 w-4 mr-2"></i>Visit DCI Page
                  </button>
                </div>
              </div>
            </div>
            
            <!-- Version History -->
            <div class="border border-gray-200 rounded-md p-6 mb-8">
              <h3 class="text-xl font-semibold text-gray-800 mb-4 flex items-center">
                <i class="fas fa-code-branch h-5 w-5 mr-2"></i>Version History
              </h3>
              <div class="space-y-4">
                <DciVersionItem 
                  :version="{ 
                    number: '2.0', 
                    description: 'Final submission with revisions', 
                    date: 'October 15, 2023', 
                    isCurrent: true, 
                    changes: [
                      'Updated methodology section based on feedback',
                      'Enhanced literature review',
                      'Added new experimental results'
                    ]
                  }"
                />
                <DciVersionItem 
                  :version="{ 
                    number: '1.1', 
                    description: 'Minor revisions from lecturer feedback', 
                    date: 'October 1, 2023',
                    isCurrent: false
                  }"
                />
                <DciVersionItem 
                  :version="{ 
                    number: '1.0', 
                    description: 'Initial submission', 
                    date: 'September 15, 2023',
                    isCurrent: false
                  }"
                />
              </div>
            </div>
            
            <!-- Verification Details -->
            <div class="border border-gray-200 rounded-md p-6 mb-8">
              <h3 class="text-xl font-semibold text-gray-800 mb-4">Verification Details</h3>
              <dl class="grid grid-cols-1 gap-x-4 gap-y-6 sm:grid-cols-2">
                <div class="sm:col-span-1">
                  <dt class="text-sm font-medium text-gray-500">AI Verification</dt>
                  <dd class="mt-1 text-sm text-gray-900 flex items-center">
                    <i class="fas fa-check-circle h-4 w-4 text-green-500 mr-1"></i>Approved on Oct 12, 2023
                  </dd>
                </div>
                <div class="sm:col-span-1">
                  <dt class="text-sm font-medium text-gray-500">Originality Score</dt>
                  <dd class="mt-1 text-sm text-gray-900">92%</dd>
                </div>
                <div class="sm:col-span-1">
                  <dt class="text-sm font-medium text-gray-500">Institution Verification</dt>
                  <dd class="mt-1 text-sm text-gray-900 flex items-center">
                    <i class="fas fa-check-circle h-4 w-4 text-green-500 mr-1"></i>Approved on Oct 14, 2023
                  </dd>
                </div>
                <div class="sm:col-span-1">
                  <dt class="text-sm font-medium text-gray-500">Institution Reviewer</dt>
                  <dd class="mt-1 text-sm text-gray-900">Dr. Sarah Johnson</dd>
                </div>
                <div class="sm:col-span-1">
                  <dt class="text-sm font-medium text-gray-500">Supervisor Verification</dt>
                  <dd class="mt-1 text-sm text-gray-900 flex items-center">
                    <i class="fas fa-check-circle h-4 w-4 text-green-500 mr-1"></i>Approved on Oct 15, 2023
                  </dd>
                </div>
                <div class="sm:col-span-1">
                  <dt class="text-sm font-medium text-gray-500">DCI Issuance Date</dt>
                  <dd class="mt-1 text-sm text-gray-900">October 15, 2023</dd>
                </div>
              </dl>
            </div>
            
            <!-- Blockchain Verification -->
            <div class="border border-gray-200 rounded-md p-6 mb-8">
              <h3 class="text-xl font-semibold text-gray-800 mb-4">Blockchain Verification</h3>
              <dl>
                <div>
                  <dt class="text-sm font-medium text-gray-500">Content Hash</dt>
                  <dd class="mt-1 text-sm text-gray-900 font-mono break-all">8e4c7be93f1b9afd64e4c2b3a8e3c8b5a2f6e9d1c7b4a8e5f2d3a6c9b8e7f4d1</dd>
                </div>
                <div class="mt-4">
                  <dt class="text-sm font-medium text-gray-500">Blockchain Transaction</dt>
                  <dd class="mt-1 text-sm text-gray-900 font-mono break-all">0x7d5a9c6b4e3f2d1a8c7b6e5f4d3a2c1b0e9d8f7e6d5c4b3a2f1e0d9c8b7a6</dd>
                </div>
              </dl>
            </div>
            
            <!-- Verification Instructions -->
            <div class="text-center mb-8">
              <p class="text-sm text-gray-500">
                To verify this certificate, visit <span class="text-blue-600">verify.dci.edu</span> and enter the DCI number.
              </p>
            </div>
            
            <!-- Certificate Action Buttons -->
            <div class="flex justify-center">
              <div class="flex space-x-4">
                <button type="button" class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                  <i class="fas fa-download h-4 w-4 mr-2"></i>Download Certificate
                </button>
                <button type="button" class="inline-flex items-center px-4 py-2 border border-gray-300 shadow-sm text-sm font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                  <i class="fas fa-share h-4 w-4 mr-2"></i>Share Certificate
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Citation Formats -->
      <div class="bg-white shadow overflow-hidden sm:rounded-lg mb-8">
        <div class="px-4 py-5 sm:px-6">
          <h3 class="text-lg leading-6 font-medium text-gray-900">Citation Formats</h3>
          <p class="mt-1 max-w-2xl text-sm text-gray-500">Use these citations when referencing your work.</p>
        </div>
        <div class="border-t border-gray-200">
          <div class="px-4 py-5 sm:p-6">
            <div class="space-y-6">
              <DciCitationFormat 
                title="APA Format" 
                content="Smith, J. (2023). Advanced Machine Learning Approaches for Natural Language Processing. University of Technology. DCI-2023-10-15-78912."
              />
              <DciCitationFormat 
                title="MLA Format" 
                content="Smith, Jane. &quot;Advanced Machine Learning Approaches for Natural Language Processing.&quot; University of Technology, 2023. DCI-2023-10-15-78912."
              />
              <DciCitationFormat 
                title="Chicago Format" 
                content="Smith, Jane. 2023. &quot;Advanced Machine Learning Approaches for Natural Language Processing.&quot; University of Technology. DCI-2023-10-15-78912."
              />
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
          <i class="fas fa-arrow-left mr-2"></i> Back to Institution Review
        </button>
      </div>
    </div>
</template>
  
<script setup>
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
  </script>