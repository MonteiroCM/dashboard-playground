<script setup>
import { ref, watch } from 'vue'
import {
  DashboardLayout,
  Header,
  Sidebar,
  CardDashboard
} from './components'

// Estado do dashboard
const sidebarOpen = ref(false)
const currentView = ref('dashboard')
const currentTheme = ref('dark')

// Dados simulados para o dashboard
const stats = ref([
  { title: 'Vendas Totais', value: 'R$ 45.231', change: '+20.1%', changeType: 'positive', icon: '💰', color: 'success' },
  { title: 'Usuários Ativos', value: '2.345', change: '+15.3%', changeType: 'positive', icon: '👥', color: 'info' },
  { title: 'Taxa de Conversão', value: '3.24%', change: '+2.1%', changeType: 'positive', icon: '📈', color: 'warning' },
  { title: 'Receita Mensal', value: 'R$ 12.450', change: '-1.2%', changeType: 'negative', icon: '💳', color: 'error' }
])

const navigation = [
  { name: 'Dashboard', icon: '📊', view: 'dashboard' },
  { name: 'Vendas', icon: '💰', view: 'sales' },
  { name: 'Usuários', icon: '👥', view: 'users' },
  { name: 'Relatórios', icon: '📋', view: 'reports' },
  { name: 'Configurações', icon: '⚙️', view: 'settings' }
]

const toggleSidebar = () => {
  sidebarOpen.value = !sidebarOpen.value
}

const closeSidebar = () => {
  sidebarOpen.value = false
}

const changeView = (view) => {
  currentView.value = view
  if (window.innerWidth < 1024) {
    closeSidebar()
  }
}

const changeTheme = (theme) => {
  currentTheme.value = theme
  document.documentElement.setAttribute('data-theme', theme)
}

// Aplicar tema inicial
changeTheme(currentTheme.value)
</script>

<template>
  <div class="min-h-screen bg-base-100">
    <DashboardLayout 
      :sidebarOpen="sidebarOpen"
      @update:sidebarOpen="(value) => sidebarOpen = value"
    >
      <template #header>
        <Header 
          :currentView="currentView"
          :navigation="navigation"
          :currentTheme="currentTheme"
          :sidebarOpen="sidebarOpen"
          @changeTheme="changeTheme"
          @toggleSidebar="toggleSidebar"
        />
      </template>
      
      <template #content>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
          <CardDashboard 
            v-for="stat in stats" 
            :key="stat.title"
            :title="stat.title"
            :value="stat.value"
            :icon="stat.icon"
            :change="stat.change"
            :color="stat.color"
          />
        </div>
        
        <div class="card bg-base-100 shadow-xl">
          <div class="card-body">
            <h2 class="card-title text-outline">Bem-vindo ao Dashboard</h2>
            <p class="text-base-content/70">
              Este é um dashboard de exemplo com sidebar toggle funcional.
            </p>
            <div class="card-actions justify-start mt-4">
              <button class="btn btn-primary">Começar</button>
              <button class="btn btn-ghost">Saiba Mais</button>
            </div>
          </div>
        </div>
      </template>
      
      <template #sidebar>
        <Sidebar 
          :navigation="navigation"
          :currentView="currentView"
          :collapsed="!sidebarOpen"
          @changeView="changeView"
          @closeSidebar="closeSidebar"
        />
      </template>
    </DashboardLayout>
  </div>
</template>

<style scoped>
</style>
