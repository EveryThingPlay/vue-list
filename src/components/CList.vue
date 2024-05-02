<script setup lang="ts">
import { onMounted, ref } from 'vue'
import CListBlock from './CListBlock.vue'

const numbers = ref<Array<number>>([])

const length = Math.floor(Math.random() * 10) + 10

const list = ref<HTMLElement>()
const freeze = ref(true)

onMounted(() => {
  generateNumbers()
  updater()
  // checkVisibility();
})

function handleScroll() {
  if (!list.value)
    return

  if (list.value.offsetTop <= document.documentElement.scrollTop || list.value.offsetTop >= document.documentElement.scrollTop + document.documentElement.clientHeight)
    freeze.value = true
  else
    freeze.value = false
}

onMounted(handleScroll)

window.addEventListener('scroll', handleScroll)

function generateNumbers() {
  for (let i = 0; i < length; i++)
    numbers.value.push(Math.floor(Math.random() * length))
}

function updater() {
  setInterval(() => {
    if (!freeze.value) {
      const randomIndex = Math.floor(Math.random() * numbers.value.length)
      numbers.value[randomIndex] = Math.floor(Math.random() * length)
    }
  }, 1000)
}
</script>

<template>
  <div ref="list" class="flex flex-row gap-2">
    <CListBlock v-for="[index, k] of numbers.entries()" :key="index" :val="`${k}`" />
  </div>
</template>
