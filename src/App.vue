<script setup lang="ts">
import { RouterView } from 'vue-router'
import { ref } from 'vue'

import { type Cigarette } from './ts/types/cigarette'

import CigaretteButton from './components/CigaretteButton.vue'
import CigarettesList from './components/CigarettesList.vue'
import CigaretteDialog from './components/CigaretteDialog.vue'

const cigarettes = ref<Cigarette[]>([])
const currentCigarette = ref<Cigarette | undefined>(undefined)
const cigaretteDialogRef = ref<typeof CigaretteDialog | null>(null)

let tmpId = 0;

const pad = (str: string): string => {
  if (str.length === 2) return str
  return pad('0' + str);
}

const newDate = () => {
  const date = new Date()
  return date.getFullYear() +
  `-${pad(date.getMonth().toString())}` + 
  `-${pad(date.getDate().toString())}` + 
  `T${date.getHours()}:${date.getMinutes()}`
}

const addCigarette = (id: number | null = null, date: string | null = null) => {
  cigarettes.value.push({
    id: id ?? tmpId++
  , date: date ?? newDate()
  })
}

const findCigarette   = (id: number) => cigarettes.value.find((cigarette: Cigarette) => cigarette.id === id) 

const removeCigarette = (id: number) => cigarettes.value = cigarettes.value.filter(cigarette => cigarette.id !== id) 

const sortCigarettes = () => cigarettes.value.sort((a, b) => a.id - b.id)

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const addCigaretteHandler = (_: MouseEvent) => addCigarette()

const showCigaretteHandler = (event: Event) => {
  const target = event.target as HTMLInputElement
  const cigaretteId = target.dataset.id

  if (!cigaretteId)
    throw new Error('Could not find data-id')

  if (!cigaretteDialogRef.value)
    throw new Error('Could not find cigaretteDialogRef')

  currentCigarette.value = findCigarette(parseInt(cigaretteId))

  cigaretteDialogRef.value.cigaretteDialogRef.showModal()
}

const editCigaretteHandler = (id: number, date: string) => {
  removeCigarette(id)
  addCigarette(id, date)
  sortCigarettes()
}

const removeCigaretteHandler = (id: number) => removeCigarette(id)

</script>

<template>
  <header>
    <h1>Compteur de cigarettes</h1>
  </header>

  <div class="container" style="margin-top: 80px">
    <CigaretteButton
      msg="Nouvelle clope"
      :cigarettes="cigarettes"
      :addCigaretteHandler="addCigaretteHandler"
    />
    <CigarettesList
      :cigarettes="cigarettes"
      :showCigarette="showCigaretteHandler"
    />
    <CigaretteDialog 
      ref="cigaretteDialogRef"
      :cigarette="currentCigarette"
      :editCigarette="editCigaretteHandler"
      :removeCigarette="removeCigaretteHandler"
    />

    <pre><code>{{cigarettes}}</code></pre>
  </div>

  <RouterView />
</template>

<style scoped>
header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  padding: 20px;
  text-align: left;
}

h1 {
  color: #AAA;
  font-size: 1.5rem;
}
</style>
