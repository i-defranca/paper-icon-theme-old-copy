<template>
  <div class="flex h-screen justify-center items-center">
    <NuxtPage />
  </div>
</template>
<script setup lang="ts">
useHead({
  meta: [{ content: { title: 'clip-title' } }],
  titleTemplate: (title) => `clip-title | ${title}`
});
</script>
