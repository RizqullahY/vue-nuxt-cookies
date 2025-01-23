<template>
  <div class="container min-h-screen bg-gradient-to-r from-slate-600 to-slate-800 flex flex-col items-center justify-center p-6">
    <h1 class="text-4xl font-extrabold mb-6 text-gray-100 tracking-wide shadow-lg transform transition duration-500 hover:scale-105">
      IZZUDIN MUJAKI SUKA KUE
    </h1>
    <p class="text-xl mb-4 text-gray-200 font-semibold shadow-md rounded-lg px-3 py-2 hover:bg-gray-700 transition duration-300">
      Kue Lumpia
    </p>
    <p class="text-xl mb-4 text-gray-200 font-semibold shadow-md rounded-lg px-3 py-2 hover:bg-gray-700 transition duration-300">
      {{ cookieName }}
    </p>
    <p class="text-xl mb-4 text-gray-200 font-semibold shadow-md rounded-lg px-3 py-2 hover:bg-gray-700 transition duration-300">
      Kue Pukis
    </p>
    <p class="text-xl mb-4 text-gray-200 font-semibold shadow-md rounded-lg px-3 py-2 hover:bg-gray-700 transition duration-300">
      Kue Ulang Tahun
    </p>
  </div>
</template>



<script setup lang="ts">
import { useCounterStore } from "~/stores/counter";
import { cookiesList } from "~/data/cookies";

const store = useCounterStore();
const cookie = useCookie("counter", {
  default: () => 1,
  watch: true,
});

store.setCount(cookie.value);

watch(
  () => store.count,
  (newValue) => {
    cookie.value = newValue;
  }
);

const count = computed(() => store.count);
const cookieName = computed(() => {
  return cookiesList[count.value - 1] || "404 NOT FOUND.";
});
</script>

<style scoped>
body {
  transition: background-color 0.3s ease, color 0.3s ease;
}
</style>
