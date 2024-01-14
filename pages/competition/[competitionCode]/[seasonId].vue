<script lang='ts' setup>
import { useQuery } from '@tanstack/vue-query'

const route = useRoute('competition-competitionCode-seasonId')

const supabase = useTypedSupabaseClient()

const { data: table } = useQuery({
  queryKey: ['table', route.params.seasonId],
  queryFn: async () => {
    const { data, error } = await supabase
      .rpc('season_table', { p_season_id: Number(route.params.seasonId) })
    if (error)
      throw error
    return data
  },
})

const columns = [
  {
    key: 'pos',
    label: '#',
  },
  {
    key: 'team_name',
    label: 'Team',
  },
  {
    key: 'played',
    label: 'P',
  },
  {
    key: 'won',
    label: 'W',
  },
  {
    key: 'drawn',
    label: 'D',
  },
  {
    key: 'lost',
    label: 'L',
  },
  {
    key: 'goals_for',
    label: 'GF',
  },
  {
    key: 'goals_against',
    label: 'GA',
  },
  {
    key: 'goal_difference',
    label: 'GD',
  },
  {
    key: 'points',
    label: 'Pts',
  },
]
</script>

<template>
  <UTable
    :rows="table"
    :columns="columns"
  >
    <template #points-data="{ row }">
      {{ row.points }}<span class="text-red-500">{{ row.deductions === 0 ? '' : ` (-${row.deductions})` }}</span>
    </template>
  </UTable>
</template>
