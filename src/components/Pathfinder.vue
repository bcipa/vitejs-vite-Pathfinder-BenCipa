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
      continueSearch: true,
    };
  },
  methods: {
    perform(row, col) {
      let movementCount = 0;
      let queue = [[row, col]];

      while (queue.length) {
        const len = queue.length;

        for (let i = 0; i < len; i += 1) {
          const [x, y] = queue.shift();

          if (this.maze[x][y] == 'x') return movementCount;

          if (y < this.maze[0].length - 1 && this.canMove(x, y + 1)) {
            queue.push([x, y + 1]);
            this.previouslyVisitedSteps[x][y + 1] = 2;
          }

          if (x < this.maze.length - 1 && this.canMove(x + 1, y)) {
            queue.push([x + 1, y]);
            this.previouslyVisitedSteps[x][y + 1] = 2;
          }

          if (y > 0 && this.canMove(x, y - 1)) {
            queue.push([x, y - 1]);
            this.previouslyVisitedSteps[(x, y - 1] = 2;
          }

          if (x > 0 && this.canMove(x - 1, y)) {
            queue.push([x - 1, y]);
            this.previouslyVisitedSteps[x - 1, y] = 2;
          }
        }
        movementCount += 1;
      }

      return movementCount;
    },
    canMove(row, col) {
      return (
        this.maze[row][col] === 1 && this.previouslyVisitedSteps[row][col] !== 2
      );
    },
  },
  mounted() {
    // let solution = this.perform(
    //   this.enteranceCoordinates[0],
    //   this.enteranceCoordinates[1]
    // );
    //console.log(solution);
    //this.maze = this.previouslyVisitedSteps;
    //console.log(this.previouslyVisitedSteps);
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
