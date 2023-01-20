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
    perform() {
      console.log('LETS GO');

      console.log('DONE');
    },
    moveNorth() {},
    moveEast() {},
    moveSouth() {},
    moveWest() {},
  },
  mounted() {
    this.perform();
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
