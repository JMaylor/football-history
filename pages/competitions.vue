<script lang='ts' setup>
import { useQuery } from '@tanstack/vue-query'

const supabase = useTypedSupabaseClient()

const { data: competitions } = useQuery({
  queryKey: ['competitions'],
  queryFn: async () => {
    const { data, error } = await supabase
      .from('competition')
      .select('*')
      .order('competition_code')
    if (error)
      throw error
    return data
  },
})
</script>

<template>
  <h1>Competitions</h1>
  <NuxtLink
    v-for="competition in competitions"
    :key="competition.competition_code"
    :to="`/competition/${competition.competition_code}`"
  >
    {{ competition.competition_code }}
  </NuxtLink>
</template>
