<script setup lang="ts">
useHead({
  title: 'Football',
  htmlAttrs: {
    lang: 'en',
    class: 'overflow-y-scroll',
  },
  bodyAttrs: {
    class: 'bg-gray-50 dark:bg-gray-900',
  },
})
</script>

<template>
  <TheHeader />
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>
