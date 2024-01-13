<script lang='ts' setup>
import { useQuery } from '@tanstack/vue-query'

const supabase = useTypedSupabaseClient()

const { data: teams } = useQuery({
  queryKey: ['teams'],
  queryFn: async () => {
    const { data, error } = await supabase
      .from('team')
      .select('*')
      .order('team_name')
    if (error)
      throw error
    return data
  },
})
</script>

<template>
  <h1>Teams</h1>
  <p>Choose a team</p>
  <ul>
    <li
      v-for="team in teams"
      :key="team.team_name"
    >
      <NuxtLink :to="`/team/${team.team_name}`">
        {{ team.team_name }}
      </NuxtLink>
    </li>
  </ul>
</template>
