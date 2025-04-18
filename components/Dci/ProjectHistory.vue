<template>
    <div class="bg-white shadow overflow-hidden sm:rounded-md">
      <ul class="divide-y divide-gray-200">
        <DciProjectItem 
          v-for="(project, index) in projects" 
          :key="index" 
          :project="project" 
        />
      </ul>
    </div>
</template>
  
<script setup>
  import { ref } from 'vue';
  
  const projects = ref([
    {
      title: 'Advanced Machine Learning Approaches for NLP',
      status: 'Approved',
      statusColor: 'green',
      dciNumber: 'DCI-2023-10-15-78912',
      course: 'Advanced Topics in AI',
      date: 'October 15, 2023',
      hasViewButton: true
    },
    {
      title: 'Comparative Analysis of Sorting Algorithms',
      status: 'In Review',
      statusColor: 'yellow',
      dciNumber: 'DCI Pending',
      course: 'Algorithm Design',
      date: 'October 5, 2023',
      hasViewButton: false
    },
    {
      title: 'Web Security Fundamentals',
      status: 'Approved',
      statusColor: 'green',
      dciNumber: 'DCI-2023-09-20-45678',
      course: 'Cybersecurity Principles',
      date: 'September 20, 2023',
      hasViewButton: true
    }
  ]);
  </script>