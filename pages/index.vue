<template>
  <div>
    <h1>Cookie Value Text Display</h1>
    <p v-if="count === 1">This is the default text when cookie value is 1!</p>
    <p v-else-if="count === 2">You changed the cookie value to 2!</p>
    <p v-else-if="count === 3">Now the cookie value is 3!</p>
    <p v-else-if="count === 4">The cookie value has been changed to 4!</p>
    <p v-else-if="count === 5">High five! The cookie value is 5!</p>
    <p v-else-if="count === 6">You reached 6 in the cookie value!</p>
    <p v-else>The cookie value is {{ count }}!</p>

    <div class="current-value">
      <p>Current cookie value: {{ count }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useCounterStore } from '~/stores/counter'

const store = useCounterStore()
const cookie = useCookie('counter', {
  default: () => 1,
  watch: true
})

// Initialize store with cookie value
store.setCount(cookie.value)

// Watch for store changes and update cookie
watch(() => store.count, (newValue) => {
  cookie.value = newValue
})

// Computed property to get the current count
const count = computed(() => store.count)
</script>

<style scoped>
h1 {
  margin-bottom: 2rem;
  color: #2c3e50;
}

p {
  font-size: 1.2rem;
  margin: 1rem 0;
}

.current-value {
  margin-top: 2rem;
  padding: 1rem;
  background-color: #f8f9fa;
  border-radius: 8px;
}
</style>