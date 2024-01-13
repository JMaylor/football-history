<script lang='ts' setup>
import { useQuery } from '@tanstack/vue-query'

const route = useRoute('team-teamName')

const supabase = useTypedSupabaseClient()

const { data: oppositionTeams } = useQuery({
  queryKey: ['oppositionTeams', route.params.teamName],
  queryFn: async () => {
    const { data, error } = await supabase
      .rpc('get_opposition_teams', { p_team: route.params.teamName })
    if (error)
      throw error
    return data
  },
})
</script>

<template>
  <ul>
    <li
      v-for="team in oppositionTeams"
      :key="team.team_name"
    >
      <NuxtLink :to="`/team/${route.params.teamName}/head-to-head/${team.team_name}`">
        {{ team.team_name }}
      </NuxtLink>
    </li>
  </ul>
</template>
