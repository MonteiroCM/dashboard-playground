<script setup>
import ThemeSelector from './ThemeSelector.vue'

const props = defineProps({
  currentView: {
    type: String,
    required: true
  },
  navigation: {
    type: Array,
    required: true
  },
  currentTheme: {
    type: String,
    required: true
  },
  sidebarOpen: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['changeTheme', 'toggleSidebar'])

const handleToggleSidebar = () => {
  console.log('Header: Toggle sidebar clicado!')
  emit('toggleSidebar')
}

// Debug: logar props
console.log('Header - sidebarOpen:', props.sidebarOpen)
</script>

<template>
  <div class="navbar bg-base-100 shadow-lg border-b border-base-300">
    <!-- Botão de toggle do sidebar -->
    <div class="flex-none">
      <button 
        @click="handleToggleSidebar" 
        class="btn btn-square btn-ghost hover:bg-base-200 transition-colors duration-200"
        :class="{ 'bg-base-200': sidebarOpen }"
        aria-label="Toggle sidebar"
      >
        <svg 
          class="w-6 h-6" 
          fill="none" 
          stroke="currentColor" 
          viewBox="0 0 24 24"
          :class="{ 'rotate-180': sidebarOpen }"
        >
          <path 
            stroke-linecap="round" 
            stroke-linejoin="round" 
            stroke-width="2" 
            d="M4 6h16M4 12h16M4 18h16"
          ></path>
        </svg>
      </button>
    </div>
    
    <!-- Título da página atual -->
    <div class="flex-1">
      <h1 class="text-xl font-bold text-primary">
        {{ navigation.find(n => n.view === currentView)?.name }}
      </h1>
    </div>
    
    <!-- Ações do lado direito -->
    <div class="flex-none flex items-center gap-2">
      <!-- Seletor de tema -->
      <ThemeSelector 
        :currentTheme="currentTheme"
        @changeTheme="$emit('changeTheme', $event)"
      />
      
      <!-- Notificações -->
      <div class="dropdown dropdown-end">
        <div tabindex="0" role="button" class="btn btn-ghost btn-circle hover:bg-base-200">
          <div class="indicator">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-5 5v-5zM8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"></path>
            </svg>
            <span class="badge badge-xs badge-primary indicator-item"></span>
          </div>
        </div>
        <div tabindex="0" class="dropdown-content z-[1] menu p-2 shadow bg-base-100 rounded-box w-80">
          <div class="p-4">
            <h3 class="font-semibold">Notificações</h3>
            <p class="text-sm text-base-content/70">Você tem 3 notificações não lidas</p>
          </div>
        </div>
      </div>
      
      <!-- Perfil do usuário -->
      <div class="dropdown dropdown-end">
        <div tabindex="0" role="button" class="btn btn-ghost btn-circle avatar hover:bg-base-200">
          <div class="w-10 rounded-full">
            <img alt="Avatar" src="https://daisyui.com/images/stock/photo-1534528741775-53994a69daeb.jpg" />
          </div>
        </div>
        <ul tabindex="0" class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow bg-base-100 rounded-box w-52">
          <li><a>Perfil</a></li>
          <li><a>Configurações</a></li>
          <li><a>Sair</a></li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.btn svg {
  transition: transform 0.2s ease-in-out;
}
</style>
