<script lang="ts">
import { defineComponent, createApp } from 'vue';
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
        Array.from({ length: this.maze[0].length }, () => 0)
      ),
    };
  },
  methods: {
    perform(row, col) {
      if (this.maze[row][col] === 'x') {
        console.log('DONE!');
        return;
      } else if (this.maze[row][col] === 1 && this.maze[row][col] !== 2) {
        this.maze[row][col] = 2;

        if (col < this.maze[0].length - 1) {
          this.perform(row, col + 1);
        }

        if (row < this.maze.length - 1) {
          this.perform(row + 1, col);
        }

        if (col > 0) {
          this.perform(row, col - 1);
        }

        if (row > 0) {
          this.perform(row - 1, col);
        }
      }
    },
  },
  mounted() {
    this.perform(this.enteranceCoordinates[0], this.enteranceCoordinates[1]);
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
