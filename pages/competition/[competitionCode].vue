<script lang='ts' setup>
const route = useRoute('competition-competitionCode')
</script>

<template>
  <NuxtLink :to="`/competition/${route.params.competitionCode}`">
    <h2>
      {{ route.params.competitionCode }}
    </h2>
  </NuxtLink>
  <NuxtPage />
</template>
