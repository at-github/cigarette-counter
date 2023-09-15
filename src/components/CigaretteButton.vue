<script setup lang="ts">

import { type Cigarette } from '../ts/types/cigarette'

defineProps<{
  msg: string,
  cigarettes: Cigarette[],
  addCigaretteHandler: (p: MouseEvent) => void
}>();

</script>

<template>
  <div id="counter-container">
    <button id="add-cigarette-button" @click=addCigaretteHandler>{{ msg }}</button>
    <span id="count-day">{{ cigarettes.length }}</span>
  </div>
</template>

<style scoped>
#counter-container {
  position: absolute;
  top: 25%;
  left: 50%;

  width: 50vw;
  height: 75vw;

  margin-left: -25%;
}

#add-cigarette-button {
  width: 100%;
  height: 50vw;
  border-radius: 25vw;

  background-color: orange;
  font-size: 5vw;

  -webkit-tap-highlight-color: transparent; 
}

#count-day {
  display: block;
  position: relative;
  height: 5rem;
  top: -5rem;

  text-align: center;
  font-weight: bold;
}

#dialog-cigarette {
  border: 1px solid white;
}
</style>
