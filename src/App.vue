<template>
  <the-header />
  <base-grid />
</template>

<script>
import TheHeader from '@/components/TheHeader.vue';
import BaseGrid from '@/components/BaseGrid.vue';
export default {
  name: 'App',
  components: {
    TheHeader,
    BaseGrid,
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
