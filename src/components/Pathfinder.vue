<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    maze: Array,
  },
  methods: {
    perform() {
      console.log('LETS GO');

      console.log('DONE');
    },
  },
});
</script>

<template>
  <div v-for="(row, index) in maze" v-bind:key="index">
    <span v-for="(value, column) in row" v-bind:key="column">{{ value }}</span>
  </div>
</template>

<style scoped></style>
