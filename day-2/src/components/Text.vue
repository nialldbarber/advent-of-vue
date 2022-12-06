<script setup lang="ts">
interface Props {
  text: string
}

const props = defineProps<Props>()
</script>

<template>
  <p class="text-3xl">{{ props.text }}</p>
</template>
