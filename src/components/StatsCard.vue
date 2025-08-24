<script setup>
defineProps({
  title: {
    type: String,
    required: true
  },
  value: {
    type: [String, Number],
    required: true
  },
  icon: {
    type: String,
    required: true
  },
  change: {
    type: String,
    required: true
  },
  color: {
    type: String,
    default: 'primary'
  }
})
</script>

<template>
  <div class="card bg-base-100 shadow-xl">
    <div class="card-body">
      <div class="flex items-center justify-between">
        <div>
          <h2 class="card-title text-base-content/70">{{ title }}</h2>
          <p class="text-3xl font-bold text-base-content text-outline-soft">{{ value }}</p>
        </div>
        <div class="text-4xl">{{ icon }}</div>
      </div>
      <div class="card-actions justify-start mt-4">
        <div class="badge" :class="`badge-${color}`">
          {{ change }}
        </div>
        <span class="text-sm text-base-content/70">vs. mês anterior</span>
      </div>
    </div>
  </div>
</template>
