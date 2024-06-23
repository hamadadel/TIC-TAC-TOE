<template>
  <statistics-info :matches="matches" :wins="wins" />
  <the-header />
  <base-grid @winner="winner" />
</template>

<script>
import StatisticsInfo from '@/components/StatisticsInfo.vue';
import TheHeader from '@/components/TheHeader.vue';
import BaseGrid from '@/components/BaseGrid.vue';
export default {
  name: 'App',
  components: {
    TheHeader,
    BaseGrid,
    StatisticsInfo,
  },
  data() {
    return {
      matches: 0,
      wins: {
        O: 0,
        X: 0,
      },
    };
  },
  methods: {
    winner(winner) {
      this.matches++;
      this.wins[winner]++;
    },
  },
};
</script>
<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  max-width: 400px;
}
</style>
