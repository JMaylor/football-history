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

const columns = [
  {
    key: 'fixture_date',
    label: 'Date',
  },
  {
    key: 'result',
    label: 'Result',
  },
  {
    key: 'home_team_name',
    label: 'Home Team',
  },
  {
    key: 'full_time_home_goals',
    label: 'Home',
  },
  {
    key: 'full_time_away_goals',
    label: 'Away',
  },
  {
    key: 'away_team_name',
    label: 'Away Team',
  },
  {
    key: 'competition_code',
    label: 'Competition',
  },
  {
    key: 'season_name',
    label: 'Season',
  },
]
</script>

<template>
  <NuxtLink :to="`/team/${route.params.oppositionTeam}/head-to-head/${route.params.teamName}`">
    Switch Teams
  </NuxtLink>

  <UTable
    :rows="headToHead"
    :columns="columns"
  >
    <template #result-data="{ row }">
      <WDLRenderer
        :main-team="route.params.teamName"
        :row="row"
      />
    </template>

    <template #competition_code-data="{ row }">
      <NuxtLink
        :to="`/competition/${row.competition_code}`"
        class="text-primary flex items-center"
      >
        {{ row.competition_code }}
        <UIcon
          name="i-heroicons-link-16-solid"
          class="ml-2 my-auto"
        />
      </NuxtLink>
    </template>
  </UTable>
</template>
