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
    exitCoordinates() {
      for (let row = 0; row < this.maze.length; row++) {
        const col = this.maze[row].indexOf('x');
        if (col !== -1) return [row, col];
      }
    },
  },
  data() {
    return {
      previouslyVisitedSteps: Array.from({ length: this.maze.length }, () =>
        Array.from({ length: this.maze[0].length }, () => 0)
      ),
      paths: [],
    };
  },
  methods: {
    perform(startPoint, endPoint) {
      var queue = [[startPoint]];

      while (queue.length > 0) {
        var path = queue.shift();
        if (path.length == 0) {
          var pos = path;
        }
        var pos = path[path.length - 1];

        var direction = [
          [pos[0] + 1, pos[1]],
          [pos[0], pos[1] + 1],
          [pos[0] - 1, pos[1]],
          [pos[0], pos[1] - 1],
        ];

        for (var i = 0; i < direction.length; i++) {
          if (
            direction[i][0] == endPoint[0] &&
            direction[i][1] == endPoint[1]
          ) {
            return path.concat([endPoint]);
          }
          console.log(direction[i][0]);
          if (
            direction[i][0] < 0 ||
            direction[i][0] >= this.maze.length ||
            direction[i][1] < 0 ||
            direction[i][1] >= this.maze[0].length ||
            this.maze[direction[i][0]][direction[i][1]] != 1
          ) {
            continue;
          }

          this.maze[direction[i][0]][direction[i][1]] = 2;
          queue.push(path.concat([direction[i]]));
        }
      }
    },
    moveTo(row, col) {
      this.previouslyVisitedSteps[row][col] = 2;
    },
    canMove(row, col) {
      return (
        this.maze[row][col] === 1 && this.previouslyVisitedSteps[row][col] !== 2
      );
    },
  },
  mounted() {
    let solution = this.perform(
      this.enteranceCoordinates,
      this.exitCoordinates
    );

    console.log(solution);
    // this.maze = this.previouslyVisitedSteps;
    // console.log(this.previouslyVisitedSteps);
  },
});
</script>

<template>
  <Maze v-bind:maze="maze" v-bind:enteranceCoordinates="enteranceCoordinates" />
</template>
