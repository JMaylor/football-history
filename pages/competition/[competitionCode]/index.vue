<script lang='ts' setup>
import { useQuery } from '@tanstack/vue-query'

const route = useRoute('competition-competitionCode')

const supabase = useTypedSupabaseClient()

const { data: seasons } = useQuery({
  queryKey: ['seasons', route.params.competitionCode],
  queryFn: async () => {
    const { data, error } = await supabase
      .from('season')
      .select('*')
      .filter('competition_code', 'eq', route.params.competitionCode)
    if (error)
      throw error
    return data
  },
})
</script>

<template>
  <NuxtLink
    v-for="season in seasons"
    :key="season.season_id"
    :to="`/competition/${season.competition_code}/${season.season_id}`"
  >
    {{ season.season_name }}
  </NuxtLink>
</template>
