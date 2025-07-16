<template>
  <div>
    <div class="mb-8">
      <h1 class="text-3xl font-bold text-foreground mb-2">Chatbot Settings</h1>
      <p class="text-muted-foreground">Configure AI models and chatbot specific behaviors</p>
    </div>

    <!-- AI Model Settings -->
    <div class="card p-6 bg-card text-card-foreground rounded-lg shadow-sm">
      <h3 class="text-lg font-semibold text-foreground mb-4">AI Model Configuration</h3>
      
      <form @submit.prevent="saveSettings">
        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium text-foreground mb-2">Default AI Model</label>
            <select 
              v-model="settings.defaultModel"
              class="w-full px-3 py-2 border border-input rounded-lg focus:ring-2 focus:ring-primary focus:border-primary bg-background text-foreground"
            >
              <option value="GPT-4">GPT-4</option>
              <option value="GPT-3.5">GPT-3.5 Turbo</option>
              <option value="Claude">Claude</option>
            </select>
          </div>

          <div>
            <label class="block text-sm font-medium text-foreground mb-2">AI Role/Personality</label>
            <textarea 
              v-model="settings.aiRole"
              rows="4"
              class="w-full px-3 py-2 border border-input rounded-lg focus:ring-2 focus:ring-primary focus:border-primary bg-background text-foreground"
              placeholder="Define the AI's role and personality..."
            ></textarea>
          </div>
        </div>

        <div class="mt-6 flex justify-end">
          <button
            type="submit"
            class="btn btn-primary px-4 py-2"
          >
            Save Settings
          </button>
        </div>
      </form>
    </div>

    <!-- Model Performance Stats -->
    <div class="mt-8 card p-6 bg-card text-card-foreground rounded-lg shadow-sm">
      <h3 class="text-lg font-semibold text-foreground mb-4">Model Performance</h3>
      
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div v-for="stat in modelStats" :key="stat.model" class="bg-muted p-4 rounded-lg">
          <div class="flex items-center justify-between mb-2">
            <h4 class="font-medium text-foreground">{{ stat.model }}</h4>
            <span class="text-sm text-muted-foreground">{{ stat.usage }}% usage</span>
          </div>
          
          <div class="space-y-2">
            <div class="flex justify-between text-sm">
              <span class="text-muted-foreground">Avg Response Time</span>
              <span class="font-medium">{{ stat.avgResponseTime }}ms</span>
            </div>
            <div class="flex justify-between text-sm">
              <span class="text-muted-foreground">Success Rate</span>
              <span class="font-medium">{{ stat.successRate }}%</span>
            </div>
            <div class="flex justify-between text-sm">
              <span class="text-muted-foreground">Total Requests</span>
              <span class="font-medium">{{ stat.totalRequests }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: 'admin'
})

const settings = ref({
  defaultModel: 'GPT-4',
  aiRole: 'You are a helpful assistant that provides accurate and concise responses.'
})

const modelStats = ref([
  {
    model: 'GPT-4',
    usage: 45,
    avgResponseTime: 1200,
    successRate: 98.5,
    totalRequests: 5420
  },
  {
    model: 'GPT-3.5',
    usage: 35,
    avgResponseTime: 800,
    successRate: 97.2,
    totalRequests: 4230
  },
  {
    model: 'Claude',
    usage: 20,
    avgResponseTime: 950,
    successRate: 98.1,
    totalRequests: 2410
  }
])

const saveSettings = () => {
  // Here you would make an API call to save settings
  console.log('Saving chatbot settings:', settings.value)
  alert('Chatbot settings saved successfully!')
}
</script>
