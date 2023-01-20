<script lang="ts">
import { defineComponent } from 'vue';
import MazeStep from './MazeStep.vue';

export default defineComponent({
  props: {
    maze: Array,
  },
  components: {
    MazeStep,
  },
  computed: {
    isBeginning() {
      return false;
    },
  },
  methods: {
    perform() {
      console.log('LETS GO');
      this.findEnterance();
      console.log('DONE');
    },
    getEnteranceCoordinates() {
      let firstColumn = this.maze.map(function (value, index) {
        return value[0];
      });
      let startingStep = [0, firstColumn.indexOf(1)];
      console.log(this.MazeStep);
    },
  },
  mounted() {
    this.perform();
  },
});
</script>

<template>
  <div
    class="pf-maze-row"
    v-for="(row, rowIndex) in maze"
    v-bind:key="rowIndex"
  >
    <MazeStep
      v-for="(value, column) in row"
      v-bind:stepType="value"
      v-bind:isBeginning="false"
      v-bind:key="column"
      ref=""
    />
  </div>
</template>

<style scoped>
.pf-maze-row {
  display: flex;
}
</style>
