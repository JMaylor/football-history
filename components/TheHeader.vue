<script lang='ts' setup>
const colorMode = useColorMode()

const isDark = computed({
  get() {
    return colorMode.value === 'dark'
  },
  set() {
    colorMode.preference = colorMode.value === 'dark' ? 'light' : 'dark'
  },
})
</script>

<template>
  <header class="border-b h-16 border-b-gray-200 dark:border-b-gray-800 sticky top-0 backdrop-blur z-10">
    <UContainer class="p-4 flex items-center h-full">
      <span class="text-rose-500 mr-4 text-lg font-bold">Football</span>
      <nav class="flex space-x-2">
        <FNuxtLink
          to="/"
        >
          Home
        </FNuxtLink>
        <FNuxtLink to="/competitions">
          Competitions
        </FNuxtLink>
        <FNuxtLink to="/teams">
          Teams
        </FNuxtLink>
      </nav>
      <ClientOnly>
        <UTooltip
          :text="`Switch to ${isDark ? 'light' : 'dark'} mode`"
          class="ml-auto"
        >
          <UButton
            :icon="isDark ? 'i-heroicons-moon-20-solid' : 'i-heroicons-sun-20-solid'"
            size="sm"
            color="gray"
            square
            variant="ghost"
            @click="isDark = !isDark"
          />
        </UTooltip>
      </ClientOnly>
    </UContainer>
  </header>
</template>
