<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    stepType: String,
    isBeginning: Boolean,
    stepCoordinates: Array,
  },
  computed: {
    stepClass() {
      let wall = '';

      if (this.stepType === 0) {
        wall = 'is-barricade';
      }

      if (this.isBeginning) {
        wall = 'is-beginning';
      }

      if (this.stepType === 'x') {
        wall = 'is-finish';
      }

      return wall;
    },
  },
});
</script>

<template>
  <div class="pf-maze-step" v-bind:class="stepClass"></div>
</template>

<style scoped>
.pf-maze-step {
  border: 1px solid white;
  background-color: white;
  height: 3em;
  width: 3em;
}

.is-beginning {
  background-color: green;
}

.is-finish {
  background-color: red;
}

.is-barricade {
  background-color: black;
  border-color: black;
}
</style>
