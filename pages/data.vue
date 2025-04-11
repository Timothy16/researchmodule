<!-- pages/lecturer/data-collection.vue -->
<template>
    
      <div>
        <!-- Header Section -->
        <div class="mb-6 flex justify-between items-center">
        <div>
          <h1 class="text-3xl font-bold mb-2 flex items-center text-gray-800">
            <i class="fas fa-chart-bar text-blue-600 mr-2"></i>
            Data Collection
          </h1>
          <p class="text-gray-600">
            Create surveys, collect responses, and analyze data for your research.
          </p>
        </div>
        
        <div class="flex space-x-2">
          <NuxtLink to="/data-analysis" class="px-4 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 flex items-center">
            <i class="fas fa-chart-pie mr-2"></i>
            View Analysis
          </NuxtLink>
        </div>
      </div>
        
        <!-- Main Tabs -->
        <div class="flex flex-col h-full">
          <div class="w-full relative flex flex-col overflow-hidden bg-white rounded-lg shadow-md">
            <!-- Tabs Navigation -->
            <div class="border-b border-gray-200 bg-gray-50">
              <div class="flex overflow-x-auto">
                <button 
                  v-for="tab in mainTabs" 
                  :key="tab.id"
                  @click="activeMainTab = tab.id"
                  class="px-4 py-3 flex items-center whitespace-nowrap"
                  :class="activeMainTab === tab.id ? 
                    'border-b-2 border-blue-600 text-blue-600 font-medium' : 
                    'text-gray-700 hover:bg-gray-100'"
                >
                  <i :class="[tab.icon, 'mr-2']"></i>
                  {{ tab.label }}
                </button>
              </div>
            </div>
            
            <!-- Tab Content -->
            <div class="flex-grow overflow-y-auto p-6">
              <!-- Create Survey Tab -->
              <div v-if="activeMainTab === 'create'">
                <div class="mb-6">
                  <h2 class="text-xl font-semibold mb-4">Create New Survey</h2>
                  
                  <!-- Survey Details -->
                  <div class="bg-white rounded-lg border border-gray-200 p-6 mb-6">
                    <div class="space-y-4">
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-1">Survey Title</label>
                        <input type="text" v-model="newSurvey.title" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500" placeholder="Enter survey title">
                      </div>
                      
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-1">Description</label>
                        <textarea v-model="newSurvey.description" rows="3" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500" placeholder="Enter survey description"></textarea>
                      </div>
                      
                      <div class="flex flex-wrap gap-4">
                        <div class="flex-1 min-w-[250px]">
                          <label class="block text-sm font-medium text-gray-700 mb-1">Start Date</label>
                          <input type="date" v-model="newSurvey.startDate" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500">
                        </div>
                        <div class="flex-1 min-w-[250px]">
                          <label class="block text-sm font-medium text-gray-700 mb-1">End Date</label>
                          <input type="date" v-model="newSurvey.endDate" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500">
                        </div>
                      </div>
                    </div>
                  </div>
                  
                  <!-- Questions Section -->
                  <div class="bg-white rounded-lg border border-gray-200 p-6">
                    <div class="flex justify-between items-center mb-4">
                      <h3 class="text-lg font-semibold">Survey Questions</h3>
                      <button @click="addQuestion" class="px-3 py-1.5 bg-blue-600 text-white rounded-lg hover:bg-blue-700 flex items-center">
                        <i class="fas fa-plus mr-1"></i>
                        Add Question
                      </button>
                    </div>
                    
                    <!-- Questions List -->
                    <div class="space-y-6">
                      <div v-for="(question, index) in newSurvey.questions" :key="index" class="border border-gray-200 rounded-lg p-4 bg-gray-50">
                        <div class="flex justify-between items-start">
                          <div class="flex-1">
                            <div class="mb-3">
                              <label :for="`question-${index}`" class="block text-sm font-medium text-gray-700 mb-1">Question {{ index + 1 }}</label>
                              <input 
                                :id="`question-${index}`" 
                                v-model="question.text" 
                                type="text" 
                                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500" 
                                placeholder="Enter your question"
                              >
                            </div>
                            
                            <div class="mb-3">
                              <label class="block text-sm font-medium text-gray-700 mb-1">Question Type</label>
                              <select 
                                v-model="question.type" 
                                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500"
                                @change="handleQuestionTypeChange(index)"
                              >
                                <option value="multiple-choice">Multiple Choice</option>
                                <option value="text">Text Response</option>
                                <option value="rating">Rating Scale</option>
                                <option value="checkbox">Checkbox (Multiple Answers)</option>
                                <option value="dropdown">Dropdown</option>
                              </select>
                            </div>
                            
                            <!-- Options for multiple choice, checkbox, dropdown -->
                            <div v-if="['multiple-choice', 'checkbox', 'dropdown'].includes(question.type)" class="mb-3">
                              <label class="block text-sm font-medium text-gray-700 mb-1">Options</label>
                              
                              <div v-for="(option, optIndex) in question.options" :key="optIndex" class="flex items-center mb-2">
                                <input 
                                  v-model="question.options[optIndex]" 
                                  type="text" 
                                  class="flex-1 px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500" 
                                  placeholder="Option text"
                                >
                                <button 
                                  @click="removeOption(index, optIndex)" 
                                  class="ml-2 text-red-500 hover:text-red-700"
                                  :disabled="question.options.length <= 2"
                                >
                                  <i class="fas fa-trash"></i>
                                </button>
                              </div>
                              
                              <button 
                                @click="addOption(index)" 
                                class="mt-2 text-blue-600 hover:text-blue-800 text-sm"
                              >
                                <i class="fas fa-plus mr-1"></i>
                                Add Option
                              </button>
                            </div>
                            
                            <!-- Settings for rating scale -->
                            <div v-if="question.type === 'rating'" class="mb-3">
                              <label class="block text-sm font-medium text-gray-700 mb-1">Scale Range</label>
                              <div class="flex items-center space-x-2">
                                <select v-model="question.scaleMin" class="px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500">
                                  <option value="0">0</option>
                                  <option value="1">1</option>
                                </select>
                                <span class="text-gray-500">to</span>
                                <select v-model="question.scaleMax" class="px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500">
                                  <option value="5">5</option>
                                  <option value="10">10</option>
                                </select>
                              </div>
                            </div>
                            
                            <!-- Required toggle -->
                            <div class="flex items-center">
                              <input 
                                :id="`required-${index}`" 
                                v-model="question.required" 
                                type="checkbox" 
                                class="w-4 h-4 text-blue-600 border-gray-300 rounded focus:ring-blue-500"
                              >
                              <label :for="`required-${index}`" class="ml-2 text-sm text-gray-700">Required Question</label>
                            </div>
                          </div>
                          
                          <!-- Question Actions -->
                          <div class="ml-4">
                            <button 
                              @click="removeQuestion(index)" 
                              class="text-red-500 hover:text-red-700"
                              :disabled="newSurvey.questions.length <= 1"
                            >
                              <i class="fas fa-trash"></i>
                            </button>
                          </div>
                        </div>
                      </div>
                    </div>
                    
                    <!-- Save Survey Button -->
                    <div class="mt-6 flex justify-end">
                      <button @click="saveSurvey" class="px-6 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">
                        <i class="fas fa-save mr-1"></i>
                        Save Survey
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              
              <!-- My Surveys Tab -->
              <div v-if="activeMainTab === 'surveys'">
                <div class="flex justify-between items-center mb-6">
                  <h2 class="text-xl font-semibold">My Surveys</h2>
                  <button @click="activeMainTab = 'create'" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 flex items-center">
                    <i class="fas fa-plus mr-1"></i>
                    Create New
                  </button>
                </div>
                
                <!-- Surveys List -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                  <div v-for="survey in savedSurveys" :key="survey.id" class="bg-white rounded-lg border border-gray-200 shadow-sm hover:shadow-md transition-shadow">
                    <div class="p-6">
                      <div class="flex justify-between items-start">
                        <h3 class="text-lg font-semibold text-gray-800 mb-2">{{ survey.title }}</h3>
                        <span :class="getStatusClass(survey)">{{ getStatusText(survey) }}</span>
                      </div>
                      
                      <p class="text-gray-600 mb-4 line-clamp-2">{{ survey.description }}</p>
                      
                      <div class="flex items-center text-sm text-gray-500 mb-4">
                        <i class="fas fa-calendar-alt mr-1"></i>
                        <span>{{ formatDate(survey.startDate) }} - {{ formatDate(survey.endDate) }}</span>
                      </div>
                      
                      <div class="flex items-center text-sm text-gray-500 mb-4">
                        <i class="fas fa-question-circle mr-1"></i>
                        <span>{{ survey.questions.length }} questions</span>
                        <span class="mx-2">•</span>
                        <i class="fas fa-users mr-1"></i>
                        <span>{{ survey.responses }} responses</span>
                      </div>
                      
                      <div class="border-t border-gray-100 pt-4 flex justify-between">
                        <button @click="viewSurveyResults(survey.id)" class="text-blue-600 hover:text-blue-800">
                          <i class="fas fa-chart-bar mr-1"></i>
                          View Results
                        </button>
                        <div class="flex space-x-2">
                          <button class="text-gray-600 hover:text-gray-800">
                            <i class="fas fa-edit"></i>
                          </button>
                          <button class="text-gray-600 hover:text-gray-800">
                            <i class="fas fa-share-alt"></i>
                          </button>
                          <button class="text-red-500 hover:text-red-700">
                            <i class="fas fa-trash"></i>
                          </button>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
   
</template>
  
  <script setup>
  import { ref, reactive } from 'vue';
  import { useRouter } from 'vue-router';
  
  const router = useRouter();
  
  // Active tab tracking
  const activeMainTab = ref('create');
  
  // Main tabs
  const mainTabs = [
    { id: 'create', label: 'Create Survey', icon: 'fas fa-plus-circle' },
    { id: 'surveys', label: 'My Surveys', icon: 'fas fa-list' },
  ];
  
  // New survey form data
  const newSurvey = reactive({
    title: '',
    description: '',
    startDate: '',
    endDate: '',
    questions: [
      {
        text: '',
        type: 'multiple-choice',
        required: false,
        options: ['', ''],
        scaleMin: '1',
        scaleMax: '5'
      }
    ]
  });
  
  // Demo saved surveys
  const savedSurveys = ref([
    {
      id: 1,
      title: 'Student Satisfaction Survey',
      description: 'This survey aims to gather feedback from students about their learning experience and satisfaction with course materials and teaching methods.',
      startDate: '2024-02-15',
      endDate: '2024-03-15',
      questions: [
        { text: 'How satisfied are you with the course content?', type: 'rating' },
        { text: 'Which learning materials did you find most helpful?', type: 'multiple-choice' },
        { text: 'Do you have any suggestions for improvement?', type: 'text' }
      ],
      responses: 78,
      status: 'active'
    },
    {
      id: 2,
      title: 'Research Methods Evaluation',
      description: 'A survey to evaluate student understanding of research methodologies and their application in academic contexts.',
      startDate: '2024-01-10',
      endDate: '2024-02-10',
      questions: [
        { text: 'Which research method do you prefer?', type: 'multiple-choice' },
        { text: 'Rate your confidence in applying quantitative methods', type: 'rating' },
        { text: 'What challenges do you face when designing research?', type: 'text' }
      ],
      responses: 45,
      status: 'completed'
    },
    {
      id: 3,
      title: 'Academic Resource Usage',
      description: 'This survey collects data on how students utilize academic resources including the library, online databases, and study groups.',
      startDate: '2024-03-01',
      endDate: '2024-04-01',
      questions: [
        { text: 'How often do you use the university library?', type: 'multiple-choice' },
        { text: 'Which online databases do you access regularly?', type: 'checkbox' },
        { text: 'What additional resources would you find helpful?', type: 'text' }
      ],
      responses: 32,
      status: 'active'
    },
    {
      id: 4,
      title: 'Course Feedback Survey',
      description: 'End-of-semester survey to collect student feedback on course structure, content delivery, and assessment methods.',
      startDate: '2023-11-20',
      endDate: '2023-12-20',
      questions: [
        { text: 'How would you rate the overall course organization?', type: 'rating' },
        { text: 'Were the assessment methods appropriate for the content?', type: 'multiple-choice' },
        { text: 'What aspects of the course would you improve?', type: 'text' }
      ],
      responses: 93,
      status: 'completed'
    }
  ]);
  
  // Question management functions
  const addQuestion = () => {
    newSurvey.questions.push({
      text: '',
      type: 'multiple-choice',
      required: false,
      options: ['', ''],
      scaleMin: '1',
      scaleMax: '5'
    });
  };
  
  const removeQuestion = (index) => {
    if (newSurvey.questions.length > 1) {
      newSurvey.questions.splice(index, 1);
    }
  };
  
  const handleQuestionTypeChange = (index) => {
    const question = newSurvey.questions[index];
    
    // Reset options for multiple choice type questions
    if (['multiple-choice', 'checkbox', 'dropdown'].includes(question.type) && !question.options) {
      question.options = ['', ''];
    }
  };
  
  const addOption = (questionIndex) => {
    newSurvey.questions[questionIndex].options.push('');
  };
  
  const removeOption = (questionIndex, optionIndex) => {
    const options = newSurvey.questions[questionIndex].options;
    if (options.length > 2) {
      options.splice(optionIndex, 1);
    }
  };
  
  // Save survey
  const saveSurvey = () => {
    alert('Survey saved successfully!');
    // Reset form or navigate to surveys list
    activeMainTab.value = 'surveys';
  };
  
  // View survey results
  const viewSurveyResults = (surveyId) => {
    router.push(`/lecturer/data-analysis?surveyId=${surveyId}`);
  };
  
  // Helper functions
  const formatDate = (dateString) => {
    const options = { year: 'numeric', month: 'short', day: 'numeric' };
    return new Date(dateString).toLocaleDateString(undefined, options);
  };
  
  const getStatusClass = (survey) => {
    if (survey.status === 'active') {
      return 'px-2 py-1 rounded-full text-xs bg-green-100 text-green-800';
    } else if (survey.status === 'completed') {
      return 'px-2 py-1 rounded-full text-xs bg-gray-100 text-gray-800';
    } else if (survey.status === 'draft') {
      return 'px-2 py-1 rounded-full text-xs bg-yellow-100 text-yellow-800';
    }
    return '';
  };
  
  const getStatusText = (survey) => {
    return survey.status.charAt(0).toUpperCase() + survey.status.slice(1);
  };
  </script>
  
  <style scoped>
  /* Line clamp for survey descriptions */
  .line-clamp-2 {
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
  
  /* Transitions */
  button {
    transition: background-color 0.2s, color 0.2s;
  }
  
  /* Focus styling */
  input:focus, select:focus, textarea:focus {
    outline: none;
  }
  </style>