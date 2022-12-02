
<script setup>
// fetch('https://v2.jokeapi.dev/joke/christmas') ...

import { ref } from 'vue'

const setup = ref(null);
const delivery = ref(null);
const showDelivery = ref(false)


const getJoke = async () => {

  showDelivery.value = false
  setup.value = null;
  delivery.value = null;

  try {
    const response = await fetch('https://v2.jokeapi.dev/joke/christmas').then(res => res.json())
    setup.value = response.setup;
    delivery.value = response.delivery;

  } catch (error) {
    console.error(error);

    alert("HOHO Something went Wrong!!")
  }
}
getJoke();
</script>





<template>
  <div class="w-full h-full flex justify-center items-center">
    <div class="flex flex-col">
      <div data-qa="setup" v-if="setup" class="rounded-xl  bg-red-600 mt-2 p-6 text-white">{{ setup }}</div>
      <div data-qa="delivery" v-if="delivery && showDelivery" class="rounded-xl  bg-emerald-600 mt-2 p-6 text-white">{{
          delivery
      }}</div>
      <button v-if="showDelivery" @click="getJoke"
        class="bg-emerald-200 rounded-lg py-2 hover:bg-emerald-400 mt-4">Another</button>
      <button v-else-if="setup" @click="(showDelivery = true)"
        class="bg-emerald-200 rounded-lg py-2 hover:bg-emerald-400 mt-4">Tell Me!</button>

    </div>
  </div>
</template>
