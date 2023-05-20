<script setup>
import { ref } from 'vue';
import Card from './components/card.vue';


const actual = ref(1);
const max = ref(6);
const counter = ref([1, 2, 3, 4, 5, 6])


const nextList = () => {
  actual.value += 6;
  max.value += 6;
}
const prevList = () => {
  actual.value -= 6;
  max.value -= 6;
}

const increment = () => {
  actual.value++;
}
const decrement = () => {
  actual.value--;
}
// watch(counter, (next) => {
//   console.log(next);
// })
const reset = () => {
  const cards = document.querySelectorAll(".pokemon-card");
  cards.forEach((card) => {
    card.remove()
  })
};

</script>

<template>
  
  <main class="container">
    <button :disabled="actual <= 0 " @click="decrement">&lt;</button>
    <button @click="increment">></button>
    <div class="row gap-3 justify-content-center">
      <!-- <Card class="col-4" v-for="actual in max" :pokemonId="actual" :key="actual" /> -->
      <KeepAlive>
      <card class="col-4" :pokemonId="actual"/>
      <card class="col-4" :pokemonId="actual + 1"/>
      <card class="col-4" :pokemonId="actual + 2"/>
      </KeepAlive>
      <!-- <card class="col-4" :pokemonId="counter[3]"/>
      <card class="col-4" :pokemonId="counter[4]"/>
      <card class="col-4" :pokemonId="counter[5]"/> -->
    </div>
  </main>
</template>

<style scoped>
  body {
    background-color: red;
    background: linear-gradient(90deg, rgba(0,45,7,1) 8%, rgba(64,155,13,1) 36%, rgba(182,201,24,1) 100%);
  }
</style>
