<!-- components/research/UploadDocumentTab.vue -->
<template>
    <div>
      <h2 class="text-xl font-bold mb-4">Upload Document</h2>
  
      <!-- Document Upload Section -->
      <div class="bg-white rounded-lg border border-gray-200 p-6 mb-6">
        <div class="flex items-center space-x-2 mb-4">
          <i class="fas fa-file-upload w-5 h-5 text-blue-600"></i>
          <h3 class="text-lg font-semibold">Document Upload</h3>
        </div>
        <div class="border-2 border-dashed border-gray-300 rounded-lg p-8 text-center">
          <i class="fas fa-file-upload text-blue-500 text-4xl mb-3"></i>
          <p class="mb-4 text-gray-700">Drag and drop your document here, or click to browse</p>
          <button class="py-2 px-4 bg-blue-600 text-white rounded-lg hover:bg-blue-700">
            Browse Files
          </button>
        </div>
        <div class="mt-4">
          <p class="text-sm text-gray-500">Supported file formats: PDF, DOCX, TXT (Max 10MB)</p>
        </div>
      </div>
  
      <!-- Document tabs section (only visible after uploading) -->
      <div v-if="documentUploaded" class="bg-white rounded-lg border border-gray-200">
        <!-- Subtabs navigation -->
        <div class="border-b border-gray-200">
          <div class="flex">
            <button 
              v-for="tab in documentTabs" 
              :key="tab.id"
              @click="activeDocTab = tab.id"
              class="px-4 py-3 flex items-center whitespace-nowrap"
              :class="activeDocTab === tab.id ? 
                'border-b-2 border-blue-600 text-blue-600 font-medium' : 
                'text-gray-700 hover:bg-gray-100'"
            >
              <i :class="[tab.icon, 'mr-2']"></i>
              {{ tab.label }}
            </button>
          </div>
        </div>
  
        <!-- Tab contents -->
        <div class="p-6">
          <!-- Generate Questions Tab -->
          <div v-if="activeDocTab === 'questions'" class="space-y-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="text-lg font-semibold">Multiple Choice Questions</h3>
              <button class="py-1 px-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm">
                <i class="fas fa-redo mr-1"></i>
                Regenerate
              </button>
            </div>
            
            <!-- Sample MCQ Questions -->
            <div class="border border-gray-200 rounded-lg p-4 bg-gray-50">
              <p class="font-medium text-gray-800 mb-2">1. What is the main purpose of using blockchain in healthcare?</p>
              <div class="space-y-2 ml-6">
                <div class="flex items-center">
                  <input type="radio" id="q1a" name="q1" class="mr-2">
                  <label for="q1a" class="text-gray-700">To reduce administrative costs</label>
                </div>
                <div class="flex items-center">
                  <input type="radio" id="q1b" name="q1" class="mr-2">
                  <label for="q1b" class="text-gray-700">To secure patient data and improve interoperability</label>
                </div>
                <div class="flex items-center">
                  <input type="radio" id="q1c" name="q1" class="mr-2">
                  <label for="q1c" class="text-gray-700">To eliminate the need for medical professionals</label>
                </div>
                <div class="flex items-center">
                  <input type="radio" id="q1d" name="q1" class="mr-2">
                  <label for="q1d" class="text-gray-700">To increase the cost of healthcare services</label>
                </div>
              </div>
            </div>
            
            <div class="border border-gray-200 rounded-lg p-4 bg-gray-50">
              <p class="font-medium text-gray-800 mb-2">2. Which machine learning approach is best suited for medical image classification?</p>
              <div class="space-y-2 ml-6">
                <div class="flex items-center">
                  <input type="radio" id="q2a" name="q2" class="mr-2">
                  <label for="q2a" class="text-gray-700">Linear Regression</label>
                </div>
                <div class="flex items-center">
                  <input type="radio" id="q2b" name="q2" class="mr-2">
                  <label for="q2b" class="text-gray-700">Convolutional Neural Networks</label>
                </div>
                <div class="flex items-center">
                  <input type="radio" id="q2c" name="q2" class="mr-2">
                  <label for="q2c" class="text-gray-700">Decision Trees</label>
                </div>
                <div class="flex items-center">
                  <input type="radio" id="q2d" name="q2" class="mr-2">
                  <label for="q2d" class="text-gray-700">Association Rules</label>
                </div>
              </div>
            </div>
            
            <div class="border border-gray-200 rounded-lg p-4 bg-gray-50">
              <p class="font-medium text-gray-800 mb-2">3. What ethical consideration is most important when implementing AI in healthcare?</p>
              <div class="space-y-2 ml-6">
                <div class="flex items-center">
                  <input type="radio" id="q3a" name="q3" class="mr-2">
                  <label for="q3a" class="text-gray-700">Cost efficiency</label>
                </div>
                <div class="flex items-center">
                  <input type="radio" id="q3b" name="q3" class="mr-2">
                  <label for="q3b" class="text-gray-700">Processing speed</label>
                </div>
                <div class="flex items-center">
                  <input type="radio" id="q3c" name="q3" class="mr-2">
                  <label for="q3c" class="text-gray-700">Privacy and data protection</label>
                </div>
                <div class="flex items-center">
                  <input type="radio" id="q3d" name="q3" class="mr-2">
                  <label for="q3d" class="text-gray-700">Visual interface design</label>
                </div>
              </div>
            </div>
          </div>
  
          <!-- Citation Tab -->
          <div v-if="activeDocTab === 'citation'" class="space-y-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="text-lg font-semibold">Generated Citations</h3>
              <div>
                <select class="border border-gray-300 rounded-md px-3 py-1 text-sm">
                  <option>APA 7th Edition</option>
                  <option>MLA 9th Edition</option>
                  <option>Chicago</option>
                  <option>Harvard</option>
                  <option>IEEE</option>
                </select>
              </div>
            </div>
            
            <!-- Sample Citations -->
            <div class="space-y-4">
              <div class="p-4 bg-gray-50 border border-gray-200 rounded-lg">
                <p class="text-gray-800">Johnson, S. A., & Williams, R. T. (2023). Advances in machine learning applications for healthcare diagnostics. <em>Journal of Medical Informatics</em>, 56(3), 112-128. https://doi.org/10.1234/jmi.2023.56.3.112</p>
                <div class="flex justify-end mt-2">
                  <button class="text-blue-600 hover:text-blue-800 text-sm">
                    <i class="fas fa-copy mr-1"></i>
                    Copy
                  </button>
                </div>
              </div>
              
              <div class="p-4 bg-gray-50 border border-gray-200 rounded-lg">
                <p class="text-gray-800">Chen, M. L., Davis, J. P., & Thompson, K. R. (2022). Blockchain technology for secure electronic health records: A systematic review. <em>Telemedicine and e-Health</em>, 28(5), 625-641. https://doi.org/10.1234/teh.2022.28.5.625</p>
                <div class="flex justify-end mt-2">
                  <button class="text-blue-600 hover:text-blue-800 text-sm">
                    <i class="fas fa-copy mr-1"></i>
                    Copy
                  </button>
                </div>
              </div>
              
              <div class="p-4 bg-gray-50 border border-gray-200 rounded-lg">
                <p class="text-gray-800">Brown, R. A., & Garcia, L. E. (2023). Ethical considerations in AI-driven healthcare: Privacy, bias, and patient autonomy. <em>Ethics in Medicine</em>, 15(2), 78-92. https://doi.org/10.1234/em.2023.15.2.78</p>
                <div class="flex justify-end mt-2">
                  <button class="text-blue-600 hover:text-blue-800 text-sm">
                    <i class="fas fa-copy mr-1"></i>
                    Copy
                  </button>
                </div>
              </div>
            </div>
          </div>
  
          <!-- Summary Tab -->
          <div v-if="activeDocTab === 'summary'" class="space-y-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="text-lg font-semibold">Document Summary</h3>
              <button class="py-1 px-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm">
                <i class="fas fa-redo mr-1"></i>
                Regenerate
              </button>
            </div>
            
            <!-- Sample Summary -->
            <div class="p-4 bg-gray-50 border border-gray-200 rounded-lg">
              <h4 class="font-medium text-gray-800 mb-2">Executive Summary</h4>
              <p class="text-gray-700 mb-3">
                This research explores the integration of machine learning and blockchain technologies in healthcare systems, focusing on improving diagnostic accuracy, securing patient data, and addressing ethical concerns. The study analyzed 150 healthcare facilities that implemented these technologies over a three-year period, revealing a 32% improvement in diagnostic accuracy and a 58% reduction in data breaches.
              </p>
              
              <h4 class="font-medium text-gray-800 mb-2">Key Findings</h4>
              <ul class="list-disc pl-5 space-y-1 text-gray-700 mb-3">
                <li>Convolutional neural networks demonstrated 94% accuracy in medical image classification, outperforming traditional methods by 27%.</li>
                <li>Blockchain implementation reduced unauthorized access incidents by 58% while improving data sharing efficiency by 41%.</li>
                <li>Patient privacy concerns decreased by 35% after implementing secure AI-driven systems with proper consent protocols.</li>
                <li>Healthcare providers reported 43% time savings in administrative tasks, allowing more focus on patient care.</li>
              </ul>
              
              <h4 class="font-medium text-gray-800 mb-2">Conclusions</h4>
              <p class="text-gray-700">
                The research concludes that the careful integration of machine learning and blockchain technologies offers significant benefits to healthcare systems, including improved diagnostic accuracy, enhanced data security, and more efficient operations. However, continued attention to ethical considerations, particularly regarding privacy, consent, and algorithmic bias, remains essential as these technologies evolve.
              </p>
            </div>
            
            <div class="flex justify-end">
              <button class="py-2 px-4 bg-blue-600 text-white rounded-lg hover:bg-blue-700">
                <i class="fas fa-download mr-1"></i>
                Download Summary
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  // Mock state for demonstration
  const documentUploaded = ref(true); // Set to true to show the tabs section
  const activeDocTab = ref('questions');
  
  // Document tabs
  const documentTabs = [
    { id: 'questions', label: 'Generate Questions', icon: 'fas fa-question-circle' },
    { id: 'citation', label: 'Citation', icon: 'fas fa-quote-right' },
    { id: 'summary', label: 'Summary', icon: 'fas fa-file-alt' },
  ];
  </script>