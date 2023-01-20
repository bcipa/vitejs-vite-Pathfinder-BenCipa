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
  methods: {
    perform(row, column) {
      let currentRow = row;
      let currentCol = column;
      let previousRow = null;
      let previousCol = null;
      let complete = false;
    },
    checkNorth(row, col) {
      if (row === 0) return false;

      return this.maze[row - 1][col] === 1;
    },
    checkEast(row, col) {
      if (col === this.maze[row].length - 1) return false;

      return this.maze[row][col + 1] === 1;
    },
    checkSouth(row, col) {
      if (row === this.maze.length - 1) return false;

      return this.maze[row + 1][col] === 1;
    },
    checkWest(row, col) {
      if (col === 0) return false;

      return this.maze[row][col - 1] === 1;
    },
    moveNorth(row, col) {},
    moveEast(row, col) {
      currentCol += 1;
    },
    moveSouth(row, col) {},
    moveWest(row, col) {},
  },
  mounted() {
    this.perform(this.enteranceCoordinates[0], this.enteranceCoordinates[0]);
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
