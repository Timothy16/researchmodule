<template>
    <nav aria-label="Progress">
      <ol class="flex items-center">
        <DciNavStep 
        v-for="(step, index) in steps" 
        :key="index"
        :step="step"
        :is-active="index === currentStep"
        :is-complete="index < currentStep"
        :is-last="index === steps.length - 1"
        @click="onStepClick(index)"
      />
      </ol>
    </nav>
</template>
  
<script setup>
  import { computed } from 'vue';
  
  // Use the currentStep from parent if provided, otherwise default to 0
  const props = defineProps({
  modelValue: Number
});
  
const emit = defineEmits(['update:modelValue']);
const currentStep = computed(() => props.modelValue);
  const steps = [
    { name: 'Submit Work', description: 'Upload your document' },
    { name: 'AI Review', description: 'Automated plagiarism check' },
    { name: 'Supervisor Review', description: 'Review by course instructor' },
    { name: 'Institution Review', description: 'Final institutional verification' },
    { name: 'DCI Certificate', description: 'Get your digital certificate' }
  ];
  
 
  
  // Handle step click
  const onStepClick = (index) => {
    emit('update:modelValue', index);
};
</script>