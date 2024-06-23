<template>
  <section>
    <div class="player-info" :class="color">
      {{ message }}
    </div>
    <div class="grid">
      <base-cell
        v-for="(n, key) in cellsValues"
        :key="key"
        :value="cellsValues[key]"
        :marker="key"
        :winner="winner"
        @shot="listenOnShot"
      />
    </div>
    <restart-button v-show="winner || moves === 9" @reset="reset" />
  </section>
</template>

<script>
import BaseCell from '@/components/BaseCell.vue';
import RestartButton from '@/components/RestartButton.vue';

export default {
  name: 'BaseGrid',
  components: {
    BaseCell,
    RestartButton,
  },
  data() {
    return {
      winner: '',
      activePlayer: 'O',
      gameStatus: 'turn',
      color: 'turn',
      moves: 0,
      winConditions: [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9],
        [1, 4, 7],
        [2, 5, 8],
        [3, 6, 9],
        [1, 5, 9],
        [3, 5, 7],
      ],
      cellsValues: {
        1: '',
        2: '',
        3: '',
        4: '',
        5: '',
        6: '',
        7: '',
        8: '',
        9: '',
      },
    };
  },
  computed: {
    message() {
      return this.activePlayer + ' ' + this.gameStatus;
    },
  },
  methods: {
    listenOnShot(marker) {
      this.cellsValues[marker] = this.activePlayer;
      if (this.isThereAWinner()) {
        this.winner = this.activePlayer;
        this.$emit('winner', this.winner);
        this.gameStatus = this.color = 'win';
        this.fillRemainingCellsWithWinner();
        return;
      }
      this.activePlayer = this.activePlayer === 'O' ? 'X' : 'O';
      this.moves++;
    },
    isThereAWinner() {
      return this.winConditions.some((condition) => {
        const isXWinner = condition.every(
          (letter) => this.cellsValues[letter] === 'X'
        );
        const isOWinner = condition.every(
          (letter) => this.cellsValues[letter] === 'O'
        );
        return isXWinner || isOWinner;
      });
    },
    fillRemainingCellsWithWinner() {
      for (const index in this.cellsValues) {
        if (!this.cellsValues[index]) {
          this.cellsValues[index] = this.winner;
        }
      }
    },
    createNewPlayer() {
      return ['X', 'O'][Math.round(Math.random())];
    },
    reset() {
      for (const index in this.cellsValues) this.cellsValues[index] = '';
      (this.winner = ''),
        (this.activePlayer = this.createNewPlayer()),
        (this.gameStatus = this.color = 'turn');
      this.moves = 0;
    },
  },
  watch: {
    moves(value) {
      value === 9 ? (this.color = 'draw') : '';
      if (!this.winner && value === 9) {
        this.gameStatus = 'draw';
        this.$parent.matches++;
        this.winner = this.activePlayer = '';
      }
    },
  },
};
</script>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: 120px 120px 120px;
  grid-gap: 10px;
  background: #34495e;
  color: #fff;
  width: 100%;
  position: relative;
  padding: 10px;
  box-sizing: border-box;
}
.player-info {
  padding: 20px 0;
  border-top-left-radius: 50px;
  border-top-right-radius: 50px;
  font-size: 2em;
  font-weight: 800;
  color: #fff;
}

.turn {
  background-color: #ffc107;
}

.win {
  background-color: #8bc34a;
}

.draw {
  background-color: #dedede;
}
</style>
