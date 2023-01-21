<script lang="ts">
import { defineComponent } from 'vue';
import MazeStep from './MazeStep.vue';

export default defineComponent({
  props: {
    maze: Array,
    enteranceCoordinates: Array,
  },
  components: {
    MazeStep,
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
  <div class="pf-maze-row" v-for="(row, rowIndex) in maze">
    <MazeStep
      v-for="(value, columnIndex) in row"
      v-bind:stepType="value"
      v-bind:isBeginning="isEnterance([rowIndex, columnIndex])"
    />
  </div>
</template>

<style scoped>
.pf-maze-row {
  display: flex;
}
</style>
