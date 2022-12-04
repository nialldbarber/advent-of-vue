<script setup>
import { ref, watch } from 'vue'
import debounce from 'lodash.debounce'

const API = 'https://dummyjson.com/products/search?q='

const items = ref([])
const searchTerm = ref('')
const loading = ref(false)
const error = ref(false)

const findProducts = debounce(async term => {
  try {
    if (searchTerm.value === 0) return (products.value = [])
    loading.value = true
    const res = await (await fetch(API + term)).json()
    items.value = res?.products
  } catch (err) {
    error.value = true
    console.log(err)
  } finally {
    loading.value = false
  }
}, 500)

watch(searchTerm, newTerm => findProducts(newTerm))
</script>

<template>
  <div class="w-full h-full flex flex-col gap-5 justify-center items-center">
    <h1 class="text-4xl font-bold">Gift Search Bar</h1>
    <input
      type="text"
      class="p-2 border-2 border-gray-dark"
      v-model="searchTerm"
      placeholder="Start typing..."
      :disabled="loading"
    />
    <p v-if="error">Uh oh, there's been an error :(</p>
    <p v-if="loading" class="text-lg text-center">Please wait...</p>
    <ul v-else-if="!loading && items.length > 0" class="list-disc">
      <li v-for="item in items">
        {{ item.title }}
      </li>
    </ul>
  </div>
</template>
