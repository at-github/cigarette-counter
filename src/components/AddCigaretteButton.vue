<script setup lang="ts">
defineProps<{
  msg: string
}>()
</script>

<template>
  <button id="add-cigarette-button">{{ msg }}</button>
</template>

<style scoped>
#add-cigarette-button {
  background-color: orange;
  font-size: 2.5vw;
  width: 25vw;
  height: 25vw;
  border-radius: 12.5vw;
}
</style>
