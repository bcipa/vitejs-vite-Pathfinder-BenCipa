<script lang="ts">
import Pathfinder from './components/Pathfinder.vue';

export default {
  name: 'app',
  components: {
    Pathfinder,
  },
  data: function () {
    return {
      maze: [
        [0, 1, 1, 1, 1, 1, 1, 0, 0, 0],
        [0, 1, 0, 0, 0, 0, 1, 1, 1, 1],
        [1, 1, 1, 1, 1, 1, 1, 0, 0, 'x'],
        [0, 0, 1, 0, 0, 0, 1, 1, 0, 0],
        [0, 1, 1, 0, 0, 0, 0, 1, 0, 0],
        [0, 1, 0, 1, 1, 1, 1, 1, 0, 0],
        [0, 1, 1, 1, 0, 0, 1, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 1, 0, 0, 0],
      ],
    };
  },
};
</script>

<template>
  <Pathfinder v-bind:maze="maze" />
</template>

<style scoped></style>
