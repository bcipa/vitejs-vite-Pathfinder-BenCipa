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
    shortestPathDistance() {
      return this.bestPath.length - 1;
    },
    solvedMaze() {
      let bestPath = this.bestPath;
      let solvedMaze = this.maze.map(function (arr) {
        return arr.slice();
      });

      for (var i = 1; i < bestPath.length - 1; i++) {
        solvedMaze[bestPath[i][0]][bestPath[i][1]] = 2;
      }

      return solvedMaze;
    },
  },
  data() {
    return {
      bestPath: [],
      showSolution: false,
    };
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
  },
  mounted() {
    this.bestPath = this.perform(
      this.enteranceCoordinates,
      this.exitCoordinates
    );
  },
});
</script>

<template>
  <Maze v-bind:maze="maze" v-bind:enteranceCoordinates="enteranceCoordinates" />

  <button class="pf-solution-btn" v-on:click="showSolution = true">
    Show Solution
  </button>

  <div class="pf-solution" v-if="showSolution">
    <h3 class="pf-solutions-title">
      It takes only {{ shortestPathDistance }} steps to complete this maze!
    </h3>
    <Maze
      v-bind:maze="solvedMaze"
      v-bind:enteranceCoordinates="enteranceCoordinates"
    />
  </div>
</template>

<style>
.pf-solution {
  border: 1px solid green;
  margin-top: 1em;
}

.pf-solutions-title {
  color: green;
}

.pf-solution-btn {
  margin-top: 1em;
}
</style>
