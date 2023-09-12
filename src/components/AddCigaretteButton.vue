<script setup lang="ts">
import { ref } from 'vue';

type Cigarette = {
  id: number;
  date: string;
}

defineProps<{
  msg: string
}>()

const cigarettes = ref<Cigarette[]>([])

let tmpId = 0;

const addCigarette = () => cigarettes.value.push({id: tmpId++, date: 'wip'})

</script>

<template>
  <div id="counter-container">
    <button id="add-cigarette-button" @click=addCigarette>{{ msg }}</button>
    <span id="count-day">{{ cigarettes.length }}</span>
  </div>
  <ul id="cigarettes-list">
    <li v-for="cigarette in cigarettes" :key="cigarette.id">🚬</li>
  </ul>
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

#cigarettes-list {
  list-style: none;
  position: absolute;
  right: 0;
  top: 0;
}
</style>
