<template>
  <div class="min-h-screen bg-gray-50 flex flex-col items-center justify-center p-6">
    <h1 class="text-3xl font-bold mb-6 text-gray-800">
      Cookie Value Text Display
    </h1>
    <p class="text-lg mb-4 text-gray-600">
      {{ kueName }}
    </p>

    <div class="flex space-x-4">
    </div>

    <div class="mt-6 p-4 bg-white rounded-lg shadow-md">
      <p class="text-gray-700">Current cookie value: <strong>{{ count }}</strong></p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useCounterStore } from '~/stores/counter'
import { cookiesList } from '~/data/cookies'

const store = useCounterStore()
const cookie = useCookie('counter', {
  default: () => 1,
  watch: true,
})

store.setCount(cookie.value)

watch(() => store.count, (newValue) => {
  cookie.value = newValue
})

const count = computed(() => store.count)
const kueName = computed(() => {
  return cookiesList[count.value - 1] || '404 NOT FOUND.'
})

function updateCount(value: number) {
  store.setCount(value)
}
</script>

<style>
/* Tailwind CSS handles most of the styling */
</style>
