<script lang='ts' setup>
const props = defineProps<{
  mainTeam: string
  row: {
    home_team_name: string
    full_time_home_goals: number
    full_time_away_goals: number
    away_team_name: string
  }
}>()

const attrs = computed(() => {
  if (props.row.full_time_home_goals === props.row.full_time_away_goals) {
    return {
      colorClass: 'text-amber-500',
      letter: 'D',
    }
  }

  if ((props.row.home_team_name === props.mainTeam) === (props.row.full_time_home_goals > props.row.full_time_away_goals)) {
    return {
      colorClass: 'text-green-500',
      letter: 'W',
    }
  }
  return {
    colorClass: 'text-red-500',
    letter: 'L',
  }
})
</script>

<template>
  <span
    class="font-mono"
    :class="attrs.colorClass"
  >{{ attrs.letter }}</span>
</template>
