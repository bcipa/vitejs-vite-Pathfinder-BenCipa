<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    stepType: String,
    isBeginning: Boolean,
  },
  computed: {
    stepClass() {
      let step = '';

      if (this.stepType === 2) {
        step = 'is-path';
      }

      if (this.stepType === 0) {
        step = 'is-barricade';
      }

      if (this.stepType === 'x') {
        step = 'is-finish';
      }

      if (this.isBeginning) {
        step = 'is-beginning';
      }

      return step;
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

.is-barricade {
  background-color: black;
  border-color: black;
}

.is-beginning {
  background-color: green;
}

.is-finish {
  background-color: red;
}

.is-path {
  background-color: blue;
}
</style>
