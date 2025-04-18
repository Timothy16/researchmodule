<template>
    <div class="min-h-screen bg-slate-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <DciAppHeader />
        <main class="mt-8">
          <div class="bg-white shadow overflow-hidden sm:rounded-lg">
            <div class=" border-gray-200 mb-10">
              <div class="px-6 py-4">
                <DciProgressNav v-model="currentStep" />
              </div>
            </div>
            <div>
              <!-- Display different form based on current step -->
              <div v-if="currentStep === 0" class="p-6">
                <DciSubmissionForm />
              </div>
              <div v-else-if="currentStep === 1">
                <DciAIReview :step="currentStep" @updateStep="currentStep = $event" />
              </div>
              <div v-else-if="currentStep === 2">
                <DciSupervisorReview :step="currentStep" @updateStep="currentStep = $event" />
              </div>
              <div v-else-if="currentStep === 3">
                <DciInstitutionReview :step="currentStep" @updateStep="currentStep = $event"/>
              </div>
              <div v-else-if="currentStep === 4">
                <DciCertificate  :step="currentStep" @updateStep="currentStep = $event" />
              </div>
              
             
            </div>
          </div>
          <div class="mt-10">
            <h2 class="text-xl font-semibold text-gray-800 mb-4">Project History</h2>
            <DciProjectHistory />
          </div>
        </main>
      </div>
    </div>
</template>
  
<script setup>
  import { ref } from 'vue';
  
  // Define the current step (0: Submit Work, 1: AI Review, etc.)
  const currentStep = ref(0); // Setting to 1 to show the AI Review page by default
</script>