<template>
    <nav aria-label="Progress">
      <ol class="overflow-hidden">
        <DciWorkflowStep 
          v-for="(step, index) in steps" 
          :key="index"
          :step="step"
          :isLast="index === steps.length - 1"
        />
      </ol>
    </nav>
  </template>
  
  <script setup>
  const steps = [
    {
      name: 'AI Approval',
      status: 'Completed',
      state: 'completed'
    },
    {
      name: 'Supervisor Approval',
      status: 'Completed',
      state: 'completed'
    },
    {
      name: 'Institution Approval',
      status: 'In progress',
      state: 'current'
    },
    {
      name: 'Final DCI Issued',
      status: 'Pending',
      state: 'upcoming'
    }
  ];
  </script>