<script setup>
import { watch } from 'vue'

const props = defineProps({
  sidebarOpen: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['update:sidebarOpen'])

const closeSidebar = () => {
  emit('update:sidebarOpen', false)
}

watch(() => props.sidebarOpen, (newVal, oldVal) => {
  console.log('DashboardLayout - sidebarOpen mudou:', oldVal, '->', newVal)
})
</script>

<template>
  <div class="flex h-screen bg-base-100 relative overflow-hidden">
    <div 
      class="sidebar-container"
      :class="[{ 'sidebar-open': sidebarOpen, 'sidebar-closed': !sidebarOpen }, { 'desktop-collapsed': !sidebarOpen }]"
    >
      <slot name="sidebar"></slot>
    </div>

    <div 
      v-if="sidebarOpen" 
      class="fixed inset-0 bg-black bg-opacity-50 z-30 lg:hidden"
      @click="closeSidebar"
    ></div>

    <div class="flex-1 flex flex-col min-w-0">
      <slot name="header"></slot>
      <main class="flex-1 p-6 bg-base-200 overflow-auto">
        <slot name="content"></slot>
      </main>
    </div>
  </div>
</template>

<style scoped>
.sidebar-container{
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 320px;
  background-color: white;
  border-right: 1px solid #e5e7eb;
  box-shadow: 2px 0 8px rgba(0, 0, 0, 0.1);
  z-index: 40;
  overflow: hidden;
  transition: width 0.3s ease, transform 0.3s ease;
  transform: translateX(-100%);
}

.sidebar-open{ transform: translateX(0); }
.sidebar-closed{ transform: translateX(-100%); }

@media (min-width: 1024px){
  .sidebar-container{ position: static; transform: none !important; width: 320px; }
  .sidebar-container.desktop-collapsed{ width: 64px; }
}
</style>
