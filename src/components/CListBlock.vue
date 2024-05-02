<script setup lang="ts">
import { ref, watch } from 'vue'

const props = defineProps({
  val: {
    type: String,
    required: true,
  },
})

const block = ref<HTMLElement>()

watch(() => props.val, () => {
  block.value?.classList.add('animate')
  setTimeout(() => {
    block.value?.classList.remove('animate')
  }, 300)
}, { deep: true })
</script>

<template>
  <div ref="block" class="element">
    {{ val }}
  </div>
</template>

<style lang="pcss" scoped>
.element {
  @apply flex justify-center items-center text-black font-semibold hover:scale-80 duration-150 hover:duration-75 h-12 w-12 bg-blue-300 cursor-default rounded-md;
}

.animate {
  @apply bg-red-500 duration-100 scale-110;
}
</style>
