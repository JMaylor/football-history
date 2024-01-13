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
</script>

<template>
  {{ table }}
</template>
