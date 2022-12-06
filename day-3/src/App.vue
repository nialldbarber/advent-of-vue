<script setup>
import { computed } from 'vue'
import { useNow } from '@vueuse/core'
import CountdownHeader from '@/components/CountdownHeader.vue'
import CountdownSegment from '@/components/CountdownSegment.vue'

const now = useNow()
const christmas = new Date('12/25/2022 00:00:00')

// days
const days = computed(() => {
  return christmas.getDate() - now.value.getDate() - 1
})
// hours
const hours = computed(() => {
  return now.value.getHours() - 1
})
// minutes
const minutes = computed(() => {
  return 60 - now.value.getMinutes() - 1
})
// seconds
const seconds = computed(() => {
  return 60 - now.value.getSeconds() - 1
})

console.log({
  now: now.value.getSeconds(),
  xmas: christmas.getMinutes(),
})
</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      <div class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]">
        <CountdownHeader />
        <main class="flex justify-center">
          <CountdownSegment label="days" :number="days" />
          <CountdownSegment label="hours" :number="hours" />
          <CountdownSegment label="minutes" :number="minutes" />
          <CountdownSegment label="seconds" :number="seconds" />
        </main>
      </div>
      <h4 class="mt-10 text-gray-400 text-center text-sm">
        This challenge brought to you by <a href="https://vueschool.io/" class="underline">Vue School</a>
      </h4>
    </div>
  </div>
</template>

<style>
div {
  display: block;
}

body {
  @apply bg-gray-100;
}
</style>
