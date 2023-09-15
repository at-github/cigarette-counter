<script setup lang="ts">
import { ref } from 'vue';
import { type Cigarette } from '../ts/types/cigarette'

defineProps<{
  cigarette: Cigarette | undefined,
  editCigarette: Function,
  removeCigarette: Function
}>();

const cigaretteDialogRef = ref<HTMLDialogElement | null>(null)
const cigaretteNewDate = ref<string | null>()

defineExpose({
  cigaretteDialogRef
})

const cancelCigaretteDialogHandler = () => {
  cigaretteDialogRef.value.close()
}

const confirmCigaretteDialogHandler = (id: number, callback: Function) => {
  callback(id, cigaretteNewDate.value)
  cigaretteDialogRef.value.close()
}

const updateCigaretteDateHandler = (event: Event) => {
  const target = event.target as HTMLInputElement
  cigaretteNewDate.value = target.value
}

const removeCigaretteHandler = (id: number, callback: Function) => {
  callback(id, cigaretteNewDate.value)
  cigaretteDialogRef.value.close()
}
</script>

<template>
  <dialog id="dialog-cigarette" ref="cigaretteDialogRef">
    {{ cigarette?.id }}
    <input
      type="datetime-local"
      :value="cigarette?.date ?? null"
      @change=updateCigaretteDateHandler
    >

    <button
      @click="cancelCigaretteDialogHandler"
      formmethod="dialog"
    >❌</button>

    <button
      @click="() => confirmCigaretteDialogHandler(cigarette.id, editCigarette)"
      id="confirmBtn"
    >✅</button>
    <button
      @click="() => removeCigaretteHandler(cigarette.id, removeCigarette)"
      :data-id="cigarette?.id"
    >🗑️</button>
  </dialog>
</template>

<style scoped>
</style>
