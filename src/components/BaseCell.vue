<template>
  <div class="cell" @click="shot">
    {{ value }}
  </div>
</template>

<script>
export default {
  name: 'BaseCell',
  props: ['marker', 'winner', 'value'],
  emits: ['shot'],
  data() {
    return {
      canMark: true,
    };
  },
  methods: {
    shot() {
      if (!this.winner && this.canMark) {
        // this.value = this.$parent.activePlayer;
        this.canMark = false;
        this.$emit('shot', this.marker);
      }
    },
  },
  updated() {
    if (this.$parent.winner || this.$parent.moves === 0) {
      this.canMark = true;
    }
  },
};
</script>
<style scoped>
.cell {
  height: 120px;
  line-height: 120px;
  font-size: 3.5em;
  background: #2c3e50;
}
.cell:hover {
  background: #405971;
  cursor: pointer;
}
</style>
