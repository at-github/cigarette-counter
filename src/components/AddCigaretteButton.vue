<script setup lang="ts">
defineProps<{
  msg: string
}>()
</script>

<template>
  <div class="greetings">
    <button>{{ msg }}</button>
  </div>
</template>

<style scoped>
</style>
