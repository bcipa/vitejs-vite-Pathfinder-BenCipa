<script lang="ts">
import { defineComponent } from 'vue';
import Maze from './Maze.vue';

export default defineComponent({
  props: {
    maze: Array,
  },
  components: {
    Maze,
  },
  computed: {
    enteranceCoordinates() {
      let firstColumn = this.maze.map(function (value, index) {
        return value[0];
      });

      return [firstColumn.indexOf(1), 0];
    },
  },
  data() {
    return {
      previouslyVisitedSteps: Array.from({ length: this.maze.length }, () =>
        Array.from({ length: this.maze[0].length }, () => false)
      ),
    };
  },
  methods: {
    perform(row, col) {
      let currentRow = row;
      let currentCol = col;

      console.log('row: ' + row + ' Col: ' + col);

      if (this.maze[currentRow][currentCol] === 'x') {
        return;
      }

      if (this.checkNorth(currentRow, currentCol)) {
        this.moveNorth(currentRow, currentCol);
      }

      if (this.checkEast(currentRow, currentCol)) {
        this.moveEast(currentRow, currentCol);
      }

      if (this.checkSouth(currentRow, currentCol)) {
        this.moveSouth(currentRow, currentCol);
      }

      if (this.checkWest(currentRow, currentCol)) {
        this.moveWest(currentRow, currentCol);
      }
    },
    checkNorth(row, col) {
      let nextRow = row - 1;
      if (row === 0 || this.previouslyVisited(nextRow, col)) return false;

      return this.maze[nextRow][col] !== 0;
    },
    checkEast(row, col) {
      let nextCol = col + 1;
      if (
        col === this.maze[row].length - 1 ||
        this.previouslyVisited(row, nextCol)
      )
        return false;

      return this.maze[row][nextCol] !== 0;
    },
    checkSouth(row, col) {
      let nextRow = row + 1;
      if (row === this.maze.length - 1 || this.previouslyVisited(nextRow, col))
        return false;

      return this.maze[nextRow][col] !== 0;
    },
    checkWest(row, col) {
      let nextCol = col - 1;
      if (col === 0 || this.previouslyVisited(row, nextCol)) return false;

      return this.maze[row][nextCol] !== 0;
    },
    moveNorth(row, col) {
      this.updatePreviousCoordinates(row, col);
      row -= 1;
      this.perform(row, col);
    },
    moveEast(row, col) {
      this.updatePreviousCoordinates(row, col);
      col += 1;
      this.perform(row, col);
    },
    moveSouth(row, col) {
      this.updatePreviousCoordinates(row, col);
      row += 1;
      this.perform(row, col);
    },
    moveWest(row, col) {
      this.updatePreviousCoordinates(row, col);
      col -= 1;
      this.perform(row, col);
    },
    previouslyVisited(row, col) {
      return this.previouslyVisitedSteps[row][col];
    },
    updatePreviousCoordinates(row, col) {
      this.previouslyVisitedSteps[row][col] = true;
    },
  },
  mounted() {
    this.perform(this.enteranceCoordinates[0], this.enteranceCoordinates[1]);

    console.log(this.previouslyVisitedSteps);
  },
});
</script>

<template>
  <Maze v-bind:maze="maze" v-bind:enteranceCoordinates="enteranceCoordinates" />
</template>

<style scoped>
.pf-maze-row {
  display: flex;
}
</style>
