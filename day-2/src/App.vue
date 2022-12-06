<script setup>
import { ref } from 'vue'
import Button from './components/Button.vue'
import Text from './components/Text.vue'

const setup = ref('')
const delivery = ref('')
const showDelivery = ref(false)
const error = ref(false)

const fetchJoke = async () => {
  try {
    const res = await (await fetch('https://v2.jokeapi.dev/joke/christmas')).json()
    setup.value = res.setup
    delivery.value = res.delivery
  } catch (err) {
    error.value = true
    console.log(err)
  }
}
fetchJoke()

const tellMe = () => {
  if (showDelivery.value === false) {
    showDelivery.value = true
  }
}

const anotherJoke = () => {
  showDelivery.value = false
  fetchJoke()
}
</script>

<template>
  <div class="w-full h-full flex justify-center items-center">
    <div>
      <Text :text="setup" />
      <Button text="Tell me!" :fn="tellMe" button-type="blue" />
      <Text v-if="showDelivery" :text="delivery" />
      <Button v-if="showDelivery" text="Another" :fn="anotherJoke" button-type="red" />
    </div>
  </div>
</template>
