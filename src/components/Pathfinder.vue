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
    exitCoordinates() {
      for (let row = 0; row < this.maze.length; row++) {
        const col = this.maze[row].indexOf('x');
        if (col !== -1) return [row, col];
      }
    },
  },
  methods: {
    perform(startPoint, endPoint) {
      var queue = [[startPoint]];

      while (queue.length > 0) {
        var path = queue.shift();
        var posistion = path[path.length - 1];

        var directions = [
          [posistion[0] + 1, posistion[1]],
          [posistion[0], posistion[1] + 1],
          [posistion[0] - 1, posistion[1]],
          [posistion[0], posistion[1] - 1],
        ];

        for (var i = 0; i < directions.length; i++) {
          if (
            directions[i][0] == endPoint[0] &&
            directions[i][1] == endPoint[1]
          ) {
            return path.concat([endPoint]);
          }

          if (this.canMove(directions, i)) continue;

          queue.push(path.concat([directions[i]]));
        }
      }
    },
    canMove(directions, i) {
      return (
        directions[i][0] < 0 ||
        directions[i][0] >= this.maze.length ||
        directions[i][1] < 0 ||
        directions[i][1] >= this.maze[0].length ||
        this.maze[directions[i][0]][directions[i][1]] != 1
      );
    },
    animatePath(path) {
      for (var i = 1; i < path.length - 1; i++) {
        this.maze[path[i][0]][path[i][1]] = 2;
      }
    },
  },
  mounted() {
    let solution = this.perform(
      this.enteranceCoordinates,
      this.exitCoordinates
    );

    console.log(solution);

    this.animatePath(solution);
  },
});
</script>

<template>
  <Maze v-bind:maze="maze" v-bind:enteranceCoordinates="enteranceCoordinates" />
</template>
