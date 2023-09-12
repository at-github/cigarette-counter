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
  font-size: 5vw;
  width: 50vw;
  height: 50vw;
  border-radius: 25vw;
  margin-top: -25vw;
  margin-left: -25vw;
  position: absolute;
  top: 50%;
  left: 50%;
}
</style>
