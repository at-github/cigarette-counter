<script setup lang="ts">
import { ref } from 'vue';

type Cigarette = {
  id: number;
  date: string;
}

defineProps<{
  msg: string
}>();

const cigarettes = ref<Cigarette[]>([])
const dialogCigarette = ref<HTMLDialogElement | null>(null)
const currentCigarette = ref<Cigarette | undefined>(undefined)
const cigaretteDate = ref()

let tmpId = 0;

const showCigarette = (e: MouseEvent) => {
  if (e.target === null)
    return

  if (!(e.target instanceof HTMLElement))
    return

  if (dialogCigarette.value === null)
    return

  const cigaretteId = e.target?.dataset?.id
  if (cigaretteId === undefined)
    return

  currentCigarette.value = cigarettes.value.find(c => {
    return c.id == parseInt(cigaretteId, 10)
  })

  if (!currentCigarette.value)
    return

  dialogCigarette.value.showModal()
}

const closeDialog = () => {
  if (dialogCigarette.value === null)
    return

  dialogCigarette.value.close()
}

const confirmCigaretteDialog = (e: MouseEvent) => {
  e.preventDefault()

  closeDialog()
}

const cancelCigaretteDialog = (e: MouseEvent) => {
  e.preventDefault()

  closeDialog()
}

const checkBeforeAction = (e: MouseEvent) => {
  if (e.target === null)
    throw new Error('Target not found')

  if (!(e.target instanceof HTMLElement))
    throw new Error('Target not handled')

  const cigaretteId = e.target?.dataset?.id

  if (cigaretteId === undefined)
    throw new Error('Cigarette id not found')

  return parseInt(cigaretteId, 10)
}

const addCigarette = (date: string, id: number | null = null) => cigarettes.value.push({id: id ?? tmpId++, date})
const addCigaretteHandler = () => addCigarette('wip')

const removeCigarette = (cigaretteId: number) => {
  cigarettes.value = cigarettes.value.filter(c => c.id !== cigaretteId)
}
const removeCigaretteHandler = (e: MouseEvent) => {
  try {
    const cigaretteId = checkBeforeAction(e)
    removeCigarette(cigaretteId)

    closeDialog()
  } catch {
    return
  }
}

const editCigaretteHandler = (e: MouseEvent) => {
  try {
    const cigaretteId = checkBeforeAction(e)

    removeCigarette(cigaretteId)
    addCigarette(cigaretteDate.value, cigaretteId)

    cigarettes.value = cigarettes.value.sort((a, b) => a.id - b.id)

    closeDialog()
  } catch {
    return
  }
}

</script>

<template>
  <div id="counter-container">
    <button id="add-cigarette-button" @click=addCigaretteHandler>{{ msg }}</button>
    <span id="count-day">{{ cigarettes.length }}</span>
  </div>

  <ul id="cigarettes-list">
    <li
      v-for="cigarette in cigarettes"
      :key="cigarette.id"
      :data-id="cigarette.id"
      @click="showCigarette"
    >🚬</li>
  </ul>

  <dialog id="dialog-cigarette" ref="dialogCigarette">
    {{ currentCigarette }}
    <input type="date" v-model="cigaretteDate"/>
    <button
      @click="removeCigaretteHandler"
      :data-id="currentCigarette?.id"
    >🗑️</button>
    <button
      @click="editCigaretteHandler"
      :data-id="currentCigarette?.id"
    >✏️</button>
    <button
      @click="cancelCigaretteDialog"
      formmethod="dialog"
    >❌</button>

    <button
      @click="confirmCigaretteDialog"
      id="confirmBtn"
    >✅</button>
  </dialog>
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

#cigarettes-list li {
  cursor: pointer;
}

#dialog-cigarette {
  border: 1px solid white;
}
</style>
