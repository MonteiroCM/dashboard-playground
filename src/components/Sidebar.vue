<script setup>
defineProps({
  navigation: {
    type: Array,
    required: true
  },
  currentView: {
    type: String,
    required: true
  }
})

defineEmits(['changeView'])
</script>

<template>
  <div class="drawer-side">
    <label for="my-drawer-2" aria-label="close sidebar" class="drawer-overlay"></label>
    <aside class="min-h-full w-80 bg-base-200 text-base-content sidebar-transition">
      <div class="p-4 border-b border-base-300">
        <h1 class="text-2xl font-bold text-primary text-outline">Dashboard</h1>
      </div>
      
      <nav class="p-4">
        <ul class="menu menu-lg">
          <li v-for="item in navigation" :key="item.name">
            <a @click="$emit('changeView', item.view)" 
               :class="{ 'active': currentView === item.view }"
               class="flex items-center">
              <span class="text-xl mr-3">{{ item.icon }}</span>
              {{ item.name }}
            </a>
          </li>
        </ul>
      </nav>
    </aside>
  </div>
</template>
