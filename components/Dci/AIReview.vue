<template>
    <div class="p-6">
      <h2 class="text-xl font-semibold text-gray-800 mb-6">AI Review &amp; Approval</h2>
      
      <!-- Approval Workflow -->
      <div class="mb-8">
        <div class="border border-gray-200 rounded-md p-4 bg-white">
          <h3 class="text-lg font-medium text-gray-900">Approval Workflow</h3>
          <div class="mt-4">
            <DciApprovalWorkflow />
          </div>
        </div>
      </div>
      
      <!-- Analysis Cards -->
      <div class="grid grid-cols-1 gap-6 md:grid-cols-3">
        <DciAnalysisCard 
          title="Originality Score" 
          score="92%" 
          color="green"
          icon="fa-check-circle"
          description="Your work has passed the originality threshold of 80%."
        />
        
        <DciAnalysisCard 
          title="AI-Generated Content" 
          score="8%" 
          color="yellow"
          icon="fa-triangle-exclamation"
          description="AI-generated content is within acceptable limits (<15%)."
        />
        
        <DciAnalysisCard 
          title="Overall Analysis" 
          score="A+" 
          color="blue"
          icon="fa-chart-column"
          description="Excellent work quality and academic integrity."
        />
      </div>
      
      <!-- AI Feedback -->
      <div class="mt-8 bg-white shadow overflow-hidden sm:rounded-lg">
        <div class="px-4 py-5 sm:px-6">
          <h3 class="text-lg leading-6 font-medium text-gray-900">AI Feedback</h3>
        </div>
        <div class="border-t border-gray-200 px-4 py-5 sm:p-6">
          <div class="prose max-w-none">
            <h4>Strengths</h4>
            <ul class="list-disc pl-5 space-y-1">
              <li>Strong methodology and research approach</li>
              <li>Excellent use of primary sources</li>
              <li>Clear structure and argumentation</li>
              <li>Proper citation and referencing</li>
            </ul>
            
            <h4 class="mt-4">Areas for Improvement</h4>
            <ul class="list-disc pl-5 space-y-1">
              <li>Consider expanding the literature review section</li>
              <li>Some passages in section 3.2 could be clarified</li>
              <li>Check consistency in terminology throughout</li>
            </ul>
            
            <h4 class="mt-4">Similarity Matches</h4>
            <p>Three passages were flagged for similarity with existing publications:</p>
            <ul class="list-disc pl-5 space-y-1">
              <li>Page 12: 4% similarity with "Academic Integrity in Higher Education" (2020)</li>
              <li>Page 18: 3% similarity with "Research Methods in Social Sciences" (2019)</li>
              <li>Page 24: 1% similarity with your previously published work "Initial Study" (2021)</li>
            </ul>
          </div>
        </div>
      </div>
      
      <!-- Action Buttons -->
      <div class="mt-8 flex justify-end space-x-4">
        <button @click="goToPrevious" type="button" class="inline-flex items-center px-4 py-2 border border-gray-300 shadow-sm text-sm font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
          Request Re-Analysis
        </button>
        <button  @click="goToNext" type="button" class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
          Proceed to Institutional Review
        </button>
      </div>
    </div>
</template>
  
<script setup>
  // No additional setup required
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