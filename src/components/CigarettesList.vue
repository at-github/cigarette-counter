<script setup lang="ts">
import { type Cigarette } from '../ts/types/cigarette'

defineProps<{
  cigarettes: Array<Cigarette>,
  showCigarette: (p: MouseEvent) => void
}>();
</script>

<template>
  <ul id="cigarettes-list">
    <li
      v-for="cigarette in cigarettes"
      :key="cigarette.id"
      :data-id="cigarette.id"
      @click="showCigarette"
    >🚬</li>
  </ul>
</template>

<style scoped>
#cigarettes-list {
  list-style: none;
  position: absolute;
  right: 0;
  top: 0;
}

#cigarettes-list li {
  cursor: pointer;
}
</style>
