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
  methods: {
    perform() {
      console.log('LETS GO');

      console.log('DONE');
    },
  },
  mounted() {
    this.perform();
  },
});
</script>

<template>
  <Maze v-bind:maze="maze" />
</template>
