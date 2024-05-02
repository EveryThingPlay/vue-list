<script setup lang="ts">
import { reactive } from 'vue'
import CList from './components/CList.vue'

const lists = reactive<Array<InstanceType<typeof CList>>>([])

const length = 100 + Math.floor(Math.random() * 1000)
</script>

<template>
  <div class="flex flex-col gap-2">
    <CList v-for="k in length" :key="k" ref="lists" class="h-12" />
  </div>
</template>
