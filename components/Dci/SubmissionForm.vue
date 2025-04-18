<template>
    <div>
      <h2 class="text-xl font-semibold text-gray-800 mb-6">Submit Your Work for DCI Generation</h2>
      <div class="space-y-8">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Upload Your Work</label>
          <div class="mt-1 flex justify-center px-6 pt-5 pb-6 border-2 border-gray-300 border-dashed rounded-md">
            <div class="space-y-1 text-center">
              <i class="fas fa-cloud-upload-alt mx-auto h-12 w-12 text-gray-400 text-4xl mb-3"></i>
              <div class="flex text-sm text-gray-600">
                <label for="file-upload" class="relative cursor-pointer bg-white rounded-md font-medium text-blue-600 hover:text-blue-500 focus-within:outline-none focus-within:ring-2 focus-within:ring-offset-2 focus-within:ring-blue-500">
                  <span>Upload a file</span>
                  <input id="file-upload" name="file-upload" type="file" class="sr-only" />
                </label>
                <p class="pl-1">or drag and drop</p>
              </div>
              <p class="text-xs text-gray-500">PDF, DOCX, PPT up to 50MB</p>
            </div>
          </div>
        </div>
        <div class="sm:col-span-3">
            <label for="projectSelect" class="block text-sm font-medium text-gray-700">Select From Your Project</label>
            <div class="mt-1">
                <select
                id="projectSelect"
                name="projectSelect"
                v-model="formData.project"
                class="block w-full px-3 py-2 border border-gray-300 bg-white rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                >
                <option disabled value="">Please select</option>
                <option>Research Paper</option>
                <option>Presentation</option>
                <option>Case Study</option>
                <option>Thesis</option>
                </select>
            </div>
        </div>

        
        <div class="grid grid-cols-1 gap-y-6 gap-x-4 sm:grid-cols-6">
          <div class="sm:col-span-4">
            <label for="title" class="block text-sm font-medium text-gray-700">Title</label>
            <div class="mt-1">
              <input
                type="text"
                name="title"
                id="title"
                class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                placeholder="Research Project Title"
                v-model="formData.title"
              />
            </div>
          </div>
  
          <div class="sm:col-span-6">
            <label for="authors" class="block text-sm font-medium text-gray-700">Author(s)</label>
            <div class="mt-1">
              <input
                type="text"
                name="authors"
                id="authors"
                class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                placeholder="e.g. John Smith, Jane Doe"
                v-model="formData.authors"
              />
            </div>
          </div>
  
          <div class="sm:col-span-3">
            <label for="institution" class="block text-sm font-medium text-gray-700">Institution</label>
            <div class="mt-1">
              <input
                type="text"
                name="institution"
                id="institution"
                class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                placeholder="Your University/College"
                v-model="formData.institution"
              />
            </div>
          </div>
  
          <div class="sm:col-span-3">
            <label for="course" class="block text-sm font-medium text-gray-700">Course</label>
            <div class="mt-1">
              <input
                type="text"
                name="course"
                id="course"
                class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                placeholder="Course Name"
                v-model="formData.course"
              />
            </div>
          </div>
  
          <div class="sm:col-span-3">
            <label for="supervisor" class="block text-sm font-medium text-gray-700">Supervisor Name</label>
            <div class="mt-1">
              <input
                type="text"
                name="supervisor"
                id="supervisor"
                class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                placeholder="Professor Name"
                v-model="formData.supervisor"
              />
            </div>
          </div>
  
          <div class="sm:col-span-3">
            <label for="date" class="block text-sm font-medium text-gray-700">Submission Date</label>
            <div class="mt-1">
              <input
                type="date"
                name="date"
                id="date"
                class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                v-model="formData.date"
              />
            </div>
          </div>
  
          <div class="sm:col-span-6">
            <label for="keywords" class="block text-sm font-medium text-gray-700">Keywords</label>
            <div class="mt-1">
              <input
                type="text"
                name="keywords"
                id="keywords"
                class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                placeholder="Separate keywords with commas"
                v-model="formData.keywords"
              />
            </div>
          </div>
        </div>
  
        <div class="flex justify-end">
          <button
            type="button"
            class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
            @click="submitForm"
          >
            Submit for DCI Generation
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { reactive } from 'vue';
  
  const formData = reactive({
    title: '',
    authors: '',
    institution: '',
    course: '',
    supervisor: '',
    date: '',
    keywords: '',
    project: ''
  });
  
  const submitForm = () => {
    // Handle form submission logic here
    console.log('Form submitted:', formData);
    // You would typically make an API call here
  };
  </script>