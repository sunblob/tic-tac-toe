<template>
  <div>
    <div>
        Победитель: <span v-if="this.winner">{{ this.winner }}</span>
    </div>
    <div class="game-field">
      <div
        class="game-cell"
        v-for="(cell, i) in cells"
        :key="i"
        @click="checkCell(i)"
      >
        {{ cell.value }}
      </div>
    </div>
    <button @click="resetTheGame">Reset</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      winner: null,
      cells: Array(9).fill({ value: 0 }),
      isPlayerX: true,
    };
  },
  methods: {
    checkCell(i) {
      if (this.cells[i].value) {
        return;
      }
      this.$set(this.cells, i, this.isPlayerX ? { value: 1 } : { value: 2 });
      this.isPlayerX = !this.isPlayerX;
      this.checkForWinner();
    },
    checkForWinner() {
        const lines = [
          [0, 1, 2],
          [3, 4, 5],
          [6, 7, 8],
          [0, 3, 6],
          [1, 4, 7],
          [2, 5, 8],
          [0, 4, 8],
          [2, 4, 6],
        ];
        for (let i = 0; i < lines.length; i++) {
          const [a, b, c] = lines[i];
          if (
            this.cells[a].value &&
            this.cells[a].value === this.cells[b].value &&
            this.cells[b].value === this.cells[c].value
          ) {
            this.winner = this.winnerName(this.cells[a].value);
          //   this.resetTheGame()
            return;
          }
        }

      
      // TODO: fix this to use it with any array, matrix, etc 

      // for (let i = 0; i < this.cells.length - 2; i++) {
      //   if (
      //     this.cells[0].value &&
      //     this.cells[0].value === this.cells[4].value &&
      //     this.cells[8].value
      //   ) {
      //     this.winner = this.winnerName(this.cells[0].value);
      //     return;
      //   }
      //   if (
      //     this.cells[2].value &&
      //     this.cells[2].value === this.cells[4].value &&
      //     this.cells[6].value
      //   ) {
      //     this.winner = this.winnerName(this.cells[2].value);
      //     return;
      //   }

      //   if (
      //     this.cells[i].value &&
      //     this.cells[i].value === this.cells[i + 1].value &&
      //     this.cells[i + 2].value
      //   ) {
      //     this.winner = this.winnerName(this.cells[i].value);
      //     return;
      //   }
      // }
    },
    resetTheGame() {
      for (let i = 0; i < this.cells.length; i++) {
        this.$set(this.cells, i, { value: 0 });
      }
      this.winner = null;
      this.isPlayerX = true;
    },
    winnerName(value) {
      if (value === 1) {
        return "X";
      }
      return "O";
    },
  },
};
</script>

<style lang="scss" scoped>
.game-field {
  width: 500px;
  margin: 0 auto;
  background-color: #ccc;
  display: grid;
  grid-template-columns: repeat(3, 100px);
  justify-content: center;
}
.game-cell {
  height: 100px;
  border: 1px solid black;
  font-size: 50px;
}

.game-cell--checked {
  background-color: red;
}
</style>