<script lang='ts' setup>
import { useQuery } from '@tanstack/vue-query'

const route = useRoute('team-teamName-head-to-head-oppositionTeam')

const supabase = useTypedSupabaseClient()

const { data: headToHead } = useQuery({
  queryKey: ['headToHead', route.params.teamName, route.params.oppositionTeam],
  queryFn: async () => {
    const { data, error } = await supabase
      .rpc('head_to_head', { primary_team: route.params.teamName, secondary_team: route.params.oppositionTeam })
      .order('fixture_date', { ascending: false })
    if (error)
      throw error
    return data
  },
})
</script>

<template>
  <div>{{ headToHead }}</div>
  <NuxtLink :to="`/team/${route.params.oppositionTeam}/head-to-head/${route.params.teamName}`">
    Switch Teams
  </NuxtLink>
</template>
