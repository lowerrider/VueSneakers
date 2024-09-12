<template>
  <div class="flex flex-col items-center text-center max-w-72 mx-auto">
    <img
      :src="`/VueSneakers${imageUrl}`"
      alt="Info image"
      height="80"
      width="70"
    />
    <h2 class="mt-4 text-2xl font-medium">{{ title }}</h2>
    <p class="text-gray-400 mt-2">{{ description }}</p>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  description: String,
  imageUrl: String,
});
</script>

<style></style>
