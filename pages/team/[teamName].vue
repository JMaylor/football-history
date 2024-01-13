<script lang='ts' setup>
const route = useRoute('team-teamName')
</script>

<template>
  <NuxtLink :to="`/team/${route.params.teamName}`">
    <h2>
      {{ route.params.teamName }}
    </h2>
  </NuxtLink>
  <NuxtPage />
</template>
