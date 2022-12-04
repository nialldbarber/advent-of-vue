<script setup lang="ts">
interface Props {
  fn?: () => void
  buttonType?: 'red' | 'blue'
  text: string
}
const props = defineProps<Props>()
</script>

<template>
  <button
    :class="`bg-${props.buttonType}-500 hover:bg-${props.buttonType}-700 text-white font-bold py-2 px-4 rounded`"
    @click="props.fn"
    role="button"
    :name="props.text"
  >
    {{ props.text }}
  </button>
</template>
