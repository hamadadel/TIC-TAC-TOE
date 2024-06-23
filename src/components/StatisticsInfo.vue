<template>
  <h2 class="statistics">
    <span class="playerNames">X</span> has
    <span class="results">{{ wins['X'] }}</span> wins | Match
    <span class="results">{{ matches }}</span> |
    <span class="playerNames">O</span> has
    <span class="results">{{ wins['O'] }}</span> wins
  </h2>
</template>

<script>
export default {
  name: 'StatisticsInfo',
  props: ['matches', 'wins'],
};
</script>
<style>
.statistics {
  font-weight: 400;
}
.statistics .results {
  color: #00bcd4;
  font-weight: 800;
}

.statistics .playerNames {
  text-decoration: underline;
  color: #2c3e50;
}
</style>
