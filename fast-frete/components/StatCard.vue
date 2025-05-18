<template>
  <div class="bg-white rounded-xl shadow-md p-4 w-full">
    <div class="flex items-center justify-between mb-2">
      <h3 class="text-sm text-gray-500">{{ title }}</h3>
      <slot name="icon" />
    </div>
    <p class="text-xl font-bold">{{ value }}</p>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  value: [String, Number],
});
</script>
