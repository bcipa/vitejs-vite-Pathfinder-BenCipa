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
    enteranceCoordinates() {
      let firstColumn = this.maze.map(function (value, index) {
        return value[0];
      });

      return [firstColumn.indexOf(1), 0];
    },
  },
  methods: {
    isEnterance(currentCoordinates) {
      return (
        currentCoordinates.toString() === this.enteranceCoordinates.toString()
      );
    },
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
      v-for="(value, columnIndex) in row"
      v-bind:stepType="value"
      v-bind:isBeginning="isEnterance([rowIndex, columnIndex])"
      v-bind:stepCoordinates="[rowIndex, columnIndex]"
      v-bind:key="columnIndex"
    />
  </div>
</template>

<style scoped>
.pf-maze-row {
  display: flex;
}
</style>
