<!-- pages/lecturer/data-analysis.vue -->
<template>
    
      <div>
        <!-- Header Section -->
        <div class="mb-6 flex justify-between items-center">
          <div>
            <h1 class="text-3xl font-bold mb-2 flex items-center text-gray-800">
              <i class="fas fa-chart-pie text-blue-600 mr-2"></i>
              Data Analysis
            </h1>
            <p class="text-gray-600">
              View and analyze results from your data collection surveys.
            </p>
          </div>
          
          <div class="flex items-center space-x-2">
            <button class="px-4 py-2 bg-gray-100 text-gray-700 rounded-lg hover:bg-gray-200 flex items-center">
              <i class="fas fa-file-export mr-1"></i>
              Export
            </button>
            <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 flex items-center">
              <i class="fas fa-share-alt mr-1"></i>
              Share
            </button>
          </div>
        </div>
        
        <!-- Survey Info Card -->
        <div class="bg-white rounded-lg border border-gray-200 p-6 mb-6">
          <div class="flex justify-between items-start">
            <div>
              <h2 class="text-xl font-semibold text-gray-800 mb-2">{{ currentSurvey.title }}</h2>
              <p class="text-gray-600 mb-4">{{ currentSurvey.description }}</p>
              
              <div class="flex flex-wrap gap-x-6 gap-y-2 text-sm text-gray-500">
                <div class="flex items-center">
                  <i class="fas fa-calendar-alt mr-1"></i>
                  <span>{{ formatDate(currentSurvey.startDate) }} - {{ formatDate(currentSurvey.endDate) }}</span>
                </div>
                <div class="flex items-center">
                  <i class="fas fa-users mr-1"></i>
                  <span>{{ currentSurvey.responses }} Responses</span>
                </div>
                <div class="flex items-center">
                  <i class="fas fa-question-circle mr-1"></i>
                  <span>{{ currentSurvey.questions.length }} Questions</span>
                </div>
                <div class="flex items-center">
                  <i class="fas fa-clock mr-1"></i>
                  <span>Last response: {{ formatDate(currentSurvey.lastResponse) }}</span>
                </div>
              </div>
            </div>
            
            <span :class="getStatusClass(currentSurvey)">{{ getStatusText(currentSurvey) }}</span>
          </div>
        </div>
        
        <!-- Analysis Navigation Tabs -->
        <div class="bg-white rounded-lg border border-gray-200 mb-6">
          <div class="border-b border-gray-200">
            <div class="flex overflow-x-auto">
              <button 
                v-for="tab in analysisTabs" 
                :key="tab.id"
                @click="activeAnalysisTab = tab.id"
                class="px-4 py-3 flex items-center whitespace-nowrap"
                :class="activeAnalysisTab === tab.id ? 
                  'border-b-2 border-blue-600 text-blue-600 font-medium' : 
                  'text-gray-700 hover:bg-gray-100'"
              >
                <i :class="[tab.icon, 'mr-2']"></i>
                {{ tab.label }}
              </button>
            </div>
          </div>
          
          <!-- Summary Tab Content -->
          <div v-if="activeAnalysisTab === 'summary'" class="p-6">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
              <div class="bg-blue-50 border border-blue-200 rounded-lg p-4">
                <div class="flex items-center justify-between">
                  <h3 class="text-sm font-medium text-gray-500">Response Rate</h3>
                  <i class="fas fa-user-check text-blue-500"></i>
                </div>
                <div class="mt-2">
                  <div class="text-2xl font-bold text-gray-800">78%</div>
                  <div class="text-sm text-gray-500">78 of 100 invitees</div>
                </div>
              </div>
              
              <div class="bg-green-50 border border-green-200 rounded-lg p-4">
                <div class="flex items-center justify-between">
                  <h3 class="text-sm font-medium text-gray-500">Completion Rate</h3>
                  <i class="fas fa-check-circle text-green-500"></i>
                </div>
                <div class="mt-2">
                  <div class="text-2xl font-bold text-gray-800">92%</div>
                  <div class="text-sm text-gray-500">72 complete responses</div>
                </div>
              </div>
              
              <div class="bg-purple-50 border border-purple-200 rounded-lg p-4">
                <div class="flex items-center justify-between">
                  <h3 class="text-sm font-medium text-gray-500">Avg. Time to Complete</h3>
                  <i class="fas fa-stopwatch text-purple-500"></i>
                </div>
                <div class="mt-2">
                  <div class="text-2xl font-bold text-gray-800">4:25</div>
                  <div class="text-sm text-gray-500">minutes</div>
                </div>
              </div>
            </div>
            
            <div class="bg-gray-50 rounded-lg p-6 mb-8">
              <h3 class="text-lg font-semibold text-gray-800 mb-4">Response Timeline</h3>
              <!-- Placeholder for the chart -->
              <div class="h-64 bg-white border border-gray-200 rounded-lg flex items-center justify-center">
                <div class="text-center">
                  <i class="fas fa-chart-line text-blue-300 text-5xl mb-3"></i>
                  <p class="text-gray-500">Response rate over time chart</p>
                  <p class="text-sm text-gray-400">Shows daily response counts</p>
                </div>
              </div>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-4">
              <div class="bg-gray-50 rounded-lg p-6">
                <h3 class="text-lg font-semibold text-gray-800 mb-4">Respondent Demographics</h3>
                <!-- Placeholder for the chart -->
                <div class="h-64 bg-white border border-gray-200 rounded-lg flex items-center justify-center">
                  <div class="text-center">
                    <i class="fas fa-chart-pie text-blue-300 text-5xl mb-3"></i>
                    <p class="text-gray-500">Demographics pie chart</p>
                    <p class="text-sm text-gray-400">Breakdown of respondents by category</p>
                  </div>
                </div>
              </div>
              
              <div class="bg-gray-50 rounded-lg p-6">
                <h3 class="text-lg font-semibold text-gray-800 mb-4">Device Usage</h3>
                <!-- Placeholder for the chart -->
                <div class="h-64 bg-white border border-gray-200 rounded-lg flex items-center justify-center">
                  <div class="text-center">
                    <i class="fas fa-chart-bar text-blue-300 text-5xl mb-3"></i>
                    <p class="text-gray-500">Device usage bar chart</p>
                    <p class="text-sm text-gray-400">Desktop: 45%, Mobile: 55%</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Questions Tab Content -->
          <div v-if="activeAnalysisTab === 'questions'" class="p-6">
            <div class="space-y-8">
              <!-- Multiple Choice Question -->
              <div class="bg-gray-50 rounded-lg p-6">
                <div class="flex justify-between items-start mb-4">
                  <h3 class="text-lg font-semibold text-gray-800">1. How satisfied are you with the course content?</h3>
                  <span class="text-sm text-gray-500">78 responses</span>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div>
                    <!-- Placeholder for the chart -->
                    <div class="h-64 bg-white border border-gray-200 rounded-lg flex items-center justify-center">
                      <div class="text-center">
                        <i class="fas fa-chart-pie text-blue-300 text-5xl mb-3"></i>
                        <p class="text-gray-500">Response distribution chart</p>
                      </div>
                    </div>
                  </div>
                  
                  <div class="space-y-3">
                    <div class="flex items-center">
                      <div class="w-full bg-gray-200 rounded-full h-5">
                        <div class="bg-blue-600 h-5 rounded-full" style="width: 65%"></div>
                      </div>
                      <span class="ml-3 min-w-[60px] text-right">65% (51)</span>
                      <span class="ml-2 text-gray-700">Very Satisfied</span>
                    </div>
                    
                    <div class="flex items-center">
                      <div class="w-full bg-gray-200 rounded-full h-5">
                        <div class="bg-blue-400 h-5 rounded-full" style="width: 25%"></div>
                      </div>
                      <span class="ml-3 min-w-[60px] text-right">25% (20)</span>
                      <span class="ml-2 text-gray-700">Satisfied</span>
                    </div>
                    
                    <div class="flex items-center">
                      <div class="w-full bg-gray-200 rounded-full h-5">
                        <div class="bg-yellow-400 h-5 rounded-full" style="width: 7%"></div>
                      </div>
                      <span class="ml-3 min-w-[60px] text-right">7% (5)</span>
                      <span class="ml-2 text-gray-700">Neutral</span>
                    </div>
                    
                    <div class="flex items-center">
                      <div class="w-full bg-gray-200 rounded-full h-5">
                        <div class="bg-red-400 h-5 rounded-full" style="width: 3%"></div>
                      </div>
                      <span class="ml-3 min-w-[60px] text-right">3% (2)</span>
                      <span class="ml-2 text-gray-700">Dissatisfied</span>
                    </div>
                    
                    <div class="flex items-center">
                      <div class="w-full bg-gray-200 rounded-full h-5">
                        <div class="bg-red-600 h-5 rounded-full" style="width: 0%"></div>
                      </div>
                      <span class="ml-3 min-w-[60px] text-right">0% (0)</span>
                      <span class="ml-2 text-gray-700">Very Dissatisfied</span>
                    </div>
                  </div>
                </div>
                
                <div class="mt-4 border-t border-gray-200 pt-4">
                  <h4 class="font-medium text-gray-700 mb-2">Statistics</h4>
                  <div class="flex flex-wrap gap-x-6 gap-y-2">
                    <div class="text-sm">
                      <span class="text-gray-500">Average Rating:</span>
                      <span class="ml-1 font-medium text-gray-800">4.54 / 5</span>
                    </div>
                    <div class="text-sm">
                      <span class="text-gray-500">Median:</span>
                      <span class="ml-1 font-medium text-gray-800">5</span>
                    </div>
                    <div class="text-sm">
                      <span class="text-gray-500">Standard Deviation:</span>
                      <span class="ml-1 font-medium text-gray-800">0.76</span>
                    </div>
                  </div>
                </div>
              </div>
              
              <!-- Text Response Question -->
              <div class="bg-gray-50 rounded-lg p-6">
                <div class="flex justify-between items-start mb-4">
                  <h3 class="text-lg font-semibold text-gray-800">2. What aspects of the course would you improve?</h3>
                  <span class="text-sm text-gray-500">65 responses</span>
                </div>
                
                <div class="mb-4">
                  <h4 class="font-medium text-gray-700 mb-2">Common Themes</h4>
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="bg-white border border-gray-200 rounded-lg p-4">
                      <div class="flex items-center justify-between mb-2">
                        <span class="font-medium text-gray-800">More practical examples</span>
                        <span class="text-sm text-gray-500">28 mentions</span>
                      </div>
                      <div class="w-full bg-gray-200 rounded-full h-3">
                        <div class="bg-green-500 h-3 rounded-full" style="width: 43%"></div>
                      </div>
                    </div>
                    
                    <div class="bg-white border border-gray-200 rounded-lg p-4">
                      <div class="flex items-center justify-between mb-2">
                        <span class="font-medium text-gray-800">Additional study materials</span>
                        <span class="text-sm text-gray-500">19 mentions</span>
                      </div>
                      <div class="w-full bg-gray-200 rounded-full h-3">
                        <div class="bg-green-500 h-3 rounded-full" style="width: 29%"></div>
                      </div>
                    </div>
                    
                    <div class="bg-white border border-gray-200 rounded-lg p-4">
                      <div class="flex items-center justify-between mb-2">
                        <span class="font-medium text-gray-800">More interaction in lectures</span>
                        <span class="text-sm text-gray-500">14 mentions</span>
                      </div>
                      <div class="w-full bg-gray-200 rounded-full h-3">
                        <div class="bg-green-500 h-3 rounded-full" style="width: 22%"></div>
                      </div>
                    </div>
                    
                    <div class="bg-white border border-gray-200 rounded-lg p-4">
                      <div class="flex items-center justify-between mb-2">
                        <span class="font-medium text-gray-800">Better feedback on assignments</span>
                        <span class="text-sm text-gray-500">11 mentions</span>
                      </div>
                      <div class="w-full bg-gray-200 rounded-full h-3">
                        <div class="bg-green-500 h-3 rounded-full" style="width: 17%"></div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <div>
                  <h4 class="font-medium text-gray-700 mb-2">Sample Responses</h4>
                  <div class="space-y-3">
                    <div class="bg-white border border-gray-200 rounded-lg p-3">
                      <p class="text-gray-700">"I would love to see more practical examples that relate to real-world scenarios. The theoretical knowledge is excellent, but practical applications would help students understand how to apply concepts."</p>
                    </div>
                    
                    <div class="bg-white border border-gray-200 rounded-lg p-3">
                      <p class="text-gray-700">"Additional study materials would be helpful, particularly video tutorials explaining complex topics. This would benefit students with different learning styles."</p>
                    </div>
                    
                    <div class="bg-white border border-gray-200 rounded-lg p-3">
                      <p class="text-gray-700">"The lectures could be more interactive. Perhaps incorporating more discussions or group activities would make the learning experience more engaging."</p>
                    </div>
                  </div>
                  
                  <div class="mt-3 text-right">
                    <button class="text-blue-600 hover:text-blue-800 text-sm">
                      View all responses
                    </button>
                  </div>
                </div>
              </div>
              
              <!-- More questions would follow -->
            </div>
          </div>
          
          <!-- Individual Responses Tab Content -->
          <div v-if="activeAnalysisTab === 'individuals'" class="p-6">
            <div class="flex items-center justify-between mb-6">
              <h3 class="text-lg font-semibold text-gray-800">Individual Responses</h3>
              
              <div class="flex items-center space-x-2">
                <div class="relative">
                  <input type="text" class="pl-9 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500" placeholder="Search responses...">
                  <i class="fas fa-search absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400"></i>
                </div>
                
                <div>
                  <select class="px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500">
                    <option>Sort by: Latest</option>
                    <option>Sort by: Oldest</option>
                    <option>Sort by: A-Z</option>
                  </select>
                </div>
              </div>
            </div>
            
            <div class="space-y-4">
              <!-- Individual Response Cards -->
              <div v-for="response in individualResponses" :key="response.id" class="bg-white border border-gray-200 rounded-lg p-4 hover:shadow-md transition-shadow">
                <div class="flex justify-between items-center mb-3">
                  <div class="flex items-center">
                    <div class="bg-blue-100 text-blue-800 w-10 h-10 rounded-full flex items-center justify-center font-medium">
                      {{ response.name.charAt(0) }}{{ response.name.split(' ')[1]?.charAt(0) || '' }}
                    </div>
                    <div class="ml-3">
                      <h4 class="font-medium text-gray-800">{{ response.name }}</h4>
                      <p class="text-sm text-gray-500">{{ response.email }}</p>
                    </div>
                  </div>
                  
                  <div class="text-right">
                    <div class="text-sm text-gray-500">{{ formatDate(response.submittedAt) }}</div>
                    <div class="text-sm text-gray-500">{{ response.duration }} minutes to complete</div>
                  </div>
                </div>
                
                <div class="border-t border-gray-200 pt-3">
                  <button class="text-blue-600 hover:text-blue-800 text-sm">
                    View full response
                  </button>
                </div>
              </div>
            </div>
            
            <!-- Pagination -->
            <div class="mt-6 flex justify-between items-center">
              <div class="text-sm text-gray-500">
                Showing 1-5 of 78 responses
              </div>
              
              <div class="flex items-center space-x-1">
                <button class="px-3 py-1 border border-gray-300 rounded-lg text-gray-500 hover:bg-gray-50 disabled:opacity-50" disabled>
                  <i class="fas fa-chevron-left"></i>
                </button>
                <button class="px-3 py-1 bg-blue-600 text-white rounded-lg">1</button>
                <button class="px-3 py-1 border border-gray-300 rounded-lg text-gray-700 hover:bg-gray-50">2</button>
                <button class="px-3 py-1 border border-gray-300 rounded-lg text-gray-700 hover:bg-gray-50">3</button>
                <button class="px-3 py-1 border border-gray-300 rounded-lg text-gray-700 hover:bg-gray-50">...</button>
                <button class="px-3 py-1 border border-gray-300 rounded-lg text-gray-700 hover:bg-gray-50">16</button>
                <button class="px-3 py-1 border border-gray-300 rounded-lg text-gray-500 hover:bg-gray-50">
                  <i class="fas fa-chevron-right"></i>
                </button>
              </div>
            </div>
          </div>
          
          <!-- Cross-tabulation Tab Content -->
          <div v-if="activeAnalysisTab === 'crosstab'" class="p-6">
            <div class="mb-6">
              <h3 class="text-lg font-semibold text-gray-800 mb-4">Cross Tabulation Analysis</h3>
              <p class="text-gray-600 mb-4">Compare responses between different questions to identify patterns and correlations.</p>
              
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Variable 1</label>
                  <select class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500">
                    <option>How satisfied are you with the course content?</option>
                    <option>Which learning materials did you find most helpful?</option>
                    <option>What aspects of the course would you improve?</option>
                  </select>
                </div>
                
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Variable 2</label>
                  <select class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500">
                    <option>Demographics: Student Level</option>
                    <option>Demographics: Field of Study</option>
                    <option>Demographics: Prior Experience</option>
                  </select>
                </div>
              </div>
              
              <div class="mt-4 text-right">
                <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">
                  Generate Analysis
                </button>
              </div>
            </div>
            
            <!-- Sample Cross-tab Analysis -->
            <div class="bg-gray-50 rounded-lg p-6">
              <h4 class="font-medium text-gray-800 mb-4">Course Satisfaction by Student Level</h4>
              
              <!-- Placeholder for the chart -->
              <div class="h-64 bg-white border border-gray-200 rounded-lg flex items-center justify-center mb-6">
                <div class="text-center">
                  <i class="fas fa-chart-bar text-blue-300 text-5xl mb-3"></i>
                  <p class="text-gray-500">Cross-tabulation chart</p>
                  <p class="text-sm text-gray-400">Shows satisfaction levels across student groups</p>
                </div>
              </div>
              
              <!-- Data Table -->
              <div class="overflow-x-auto">
                <table class="min-w-full divide-y divide-gray-200">
                  <thead class="bg-gray-100">
                    <tr>
                      <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Student Level</th>
                      <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Very Satisfied</th>
                      <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Satisfied</th>
                      <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Neutral</th>
                      <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Dissatisfied</th>
                      <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Very Dissatisfied</th>
                    </tr>
                  </thead>
                  <tbody class="bg-white divide-y divide-gray-200">
                    <tr>
                      <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-800">Undergraduate</td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">58% (23)</td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">30% (12)</td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">10% (4)</td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">2% (1)</td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">0% (0)</td>
                    </tr>
                    <tr>
                      <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-800">Graduate</td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">72% (28)</td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">20% (8)</td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">5% (2)</td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">3% (1)</td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">0% (0)</td>
                    </tr>
                  </tbody>
                </table>
              </div>
              
              <div class="mt-4 border-t border-gray-200 pt-4">
                <h5 class="font-medium text-gray-700 mb-2">Insights</h5>
                <ul class="list-disc pl-5 text-sm text-gray-700 space-y-1">
                  <li>Graduate students show higher overall satisfaction (72% very satisfied) compared to undergraduates (58% very satisfied).</li>
                  <li>Both groups show very low dissatisfaction rates, with no respondents selecting "Very Dissatisfied".</li>
                  <li>Undergraduate students were more likely to select "Neutral" (10% vs 5% for graduates).</li>
                  <li>Statistical significance: p &lt; 0.05, indicating a meaningful difference between the groups.</li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { useRoute } from 'vue-router';
  
  const route = useRoute();
  const surveyId = route.query.surveyId;
  
  // Active tab tracking
  const activeAnalysisTab = ref('summary');
  
  // Analysis tabs
  const analysisTabs = [
    { id: 'summary', label: 'Summary', icon: 'fas fa-chart-pie' },
    { id: 'questions', label: 'Questions', icon: 'fas fa-question-circle' },
    { id: 'individuals', label: 'Individual Responses', icon: 'fas fa-user' },
    { id: 'crosstab', label: 'Cross Tabulation', icon: 'fas fa-table' },
  ];
  
  // Mock current survey data
  const currentSurvey = ref({
    id: 1,
    title: 'Student Satisfaction Survey',
    description: 'This survey aims to gather feedback from students about their learning experience and satisfaction with course materials and teaching methods.',
    startDate: '2024-02-15',
    endDate: '2024-03-15',
    lastResponse: '2024-03-12',
    questions: [
      { text: 'How satisfied are you with the course content?', type: 'rating' },
      { text: 'Which learning materials did you find most helpful?', type: 'multiple-choice' },
      { text: 'What aspects of the course would you improve?', type: 'text' }
    ],
    responses: 78,
    status: 'active'
  });
  
  // Mock individual responses for the table
  const individualResponses = ref([
    {
      id: 1,
      name: 'John Smith',
      email: 'john.smith@example.com',
      submittedAt: '2024-03-12T14:23:00',
      duration: 3.5
    },
    {
      id: 2,
      name: 'Sarah Johnson',
      email: 'sarah.j@example.com',
      submittedAt: '2024-03-11T09:45:00',
      duration: 5.2
    },
    {
      id: 3,
      name: 'Michael Chen',
      email: 'mchen@example.com',
      submittedAt: '2024-03-10T16:12:00',
      duration: 4.7
    },
    {
      id: 4,
      name: 'Emily Rodriguez',
      email: 'emily.r@example.com',
      submittedAt: '2024-03-09T11:30:00',
      duration: 2.8
    },
    {
      id: 5,
      name: 'David Wilson',
      email: 'd.wilson@example.com',
      submittedAt: '2024-03-08T15:45:00',
      duration: 6.2
    }
  ]);
  
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
  /* Smooth transitions for tab interactions */
  button {
    transition: background-color 0.2s, color 0.2s;
  }
  
  /* Improved focus states for accessibility */
  button:focus, input:focus, select:focus, textarea:focus {
    outline: none;
    box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.3);
  }
  
  /* Mobile styles */
  @media (max-width: 767px) {
    /* Make the tab container scrollable on small screens */
    .overflow-x-auto {
      -webkit-overflow-scrolling: touch;
      scrollbar-width: none; /* Firefox */
      -ms-overflow-style: none; /* IE and Edge */
    }
    
    .overflow-x-auto::-webkit-scrollbar {
      display: none; /* Chrome, Safari, Opera */
    }
    
    /* Adjust button sizes for better touch targets */
    button {
      min-height: 44px; /* Minimum touch target size */
    }
  }
  </style>