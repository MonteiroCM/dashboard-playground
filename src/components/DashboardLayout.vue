<script setup>
defineProps({
  sidebarOpen: {
    type: Boolean,
    required: true
  }
})

defineEmits(['update:sidebarOpen'])
</script>

<template>
  <div class="drawer lg:drawer-open">
    <input id="my-drawer-2" type="checkbox" class="drawer-toggle" :checked="sidebarOpen" @change="$emit('update:sidebarOpen', $event.target.checked)" />
    <div class="drawer-content flex flex-col">
      <slot name="header"></slot>
      <main class="p-6 bg-base-200 min-h-screen">
        <slot name="content"></slot>
      </main>
    </div>
    <slot name="sidebar"></slot>
  </div>
</template>
