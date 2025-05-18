<template>
  <div class="bg-white rounded-xl p-4 shadow flex items-center justify-between">
    <div>
      <p class="text-gray-500 text-sm">{{ title }}</p>
      <p class="text-xl font-bold">{{ value }}</p>
    </div>
    <div class="text-2xl">{{ icon }}</div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  value: String,
  icon: String
})
</script>
