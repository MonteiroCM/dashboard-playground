<script setup>
defineProps({
  navigation: {
    type: Array,
    required: true
  },
  currentView: {
    type: String,
    required: true
  },
  collapsed: {
    type: Boolean,
    default: false
  }
})

defineEmits(['changeView', 'closeSidebar'])
</script>

<template>
  <div class="h-full flex flex-col bg-base-100 text-base-content border-r border-base-300">
    <!-- Header do sidebar -->
    <div class="bg-base-200 border-b border-base-300" :class="collapsed ? 'p-3' : 'p-4'">
      <div class="flex items-center justify-between">
        <h1 v-if="!collapsed" class="text-2xl font-bold text-primary">Dashboard</h1>
        <button 
          @click="$emit('closeSidebar')"
          class="btn btn-sm btn-ghost lg:hidden"
          aria-label="Fechar sidebar"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
          </svg>
        </button>
      </div>
    </div>
    
    <!-- Navegação -->
    <nav class="flex-1 overflow-y-auto" :class="collapsed ? 'p-2' : 'p-3'">
      <ul class="flex flex-col gap-1">
        <li v-for="item in navigation" :key="item.name">
          <button
            type="button"
            @click="$emit('changeView', item.view)"
            :title="collapsed ? item.name : undefined"
            :class="[
              'w-full rounded-md transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-primary/40',
              currentView === item.view ? 'bg-primary text-primary-content' : 'hover:bg-base-200',
              collapsed ? 'flex items-center justify-center h-10' : 'flex items-center gap-3 px-3 py-2'
            ]"
          >
            <span class="text-xl">{{ item.icon }}</span>
            <span v-if="!collapsed" class="font-medium truncate">{{ item.name }}</span>
          </button>
        </li>
      </ul>
    </nav>
    
    <!-- Footer do sidebar -->
    <div v-if="!collapsed" class="p-3 border-t border-base-300 bg-base-200">
      <div class="text-center text-sm text-base-content/70">
        <p>Dashboard v1.0</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
/**** Estilos finos para transições suaves dos botões ****/
button { transition: background-color 0.15s ease, color 0.15s ease; }
</style>
