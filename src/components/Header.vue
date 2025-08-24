<script setup>
import ThemeSelector from './ThemeSelector.vue'

defineProps({
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
  }
})

defineEmits(['changeTheme', 'toggleSidebar'])
</script>

<template>
  <div class="navbar bg-base-100 shadow-lg border-b border-base-300">
    <div class="flex-none lg:hidden">
      <label @click="$emit('toggleSidebar')" class="btn btn-square btn-ghost">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
        </svg>
      </label>
    </div>
    
    <div class="flex-1">
      <h1 class="text-xl font-bold text-primary text-outline">
        {{ navigation.find(n => n.view === currentView)?.name }}
      </h1>
    </div>
    
    <div class="flex-none">
             <!-- Seletor de tema -->
       <ThemeSelector 
         :currentTheme="currentTheme"
         @changeTheme="$emit('changeTheme', $event)"
       />
      
      <!-- Notificações -->
      <div class="dropdown dropdown-end">
        <div tabindex="0" role="button" class="btn btn-ghost btn-circle">
          <div class="indicator">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-5 5v-5zM4.19 4.47A19.932 19.932 0 0112 2c5.514 0 9.998 2.239 13.81 5.47M19.5 8.25l-5.5 5.5-2.5-2.5M4.19 19.47A19.932 19.932 0 0112 22c5.514 0 9.998-2.239 13.81-5.47"></path>
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
        <div tabindex="0" role="button" class="btn btn-ghost btn-circle avatar">
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
