<script setup lang="ts">
interface Props {
  modelValue: string
  label: string
}

interface Emits {
  (e: 'change', modelValue: string): void
  (e: 'update', modelValue: string): void
}

const { modelValue } = defineProps<Props>()
const emit = defineEmits<Emits>()
</script>

<template>
  <label class="block">
    {{ label }}:
    <input
      class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2"
      type="text"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </label>
</template>
