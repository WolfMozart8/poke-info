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
    <button class="btn-left" :disabled="actual <= 1 " @click="decrement">&lt;</button>
    <button class="btn-right" @click="increment">></button>
    <div class="row gap-3 justify-content-center">
      <!-- <Card class="col-4" v-for="actual in max" :pokemonId="actual" :key="actual" /> -->
      <card class="col-4" :pokemonId="actual"/>
      <card class="col-4" :pokemonId="actual + 1"/>
      <card class="col-4" :pokemonId="actual + 2"/>
      <card class="col-4" :pokemonId="actual + 3"/>
      <card class="col-4" :pokemonId="actual + 4"/>
      <card class="col-4" :pokemonId="actual + 5"/>
      <!-- <card class="col-4" :pokemonId="counter[3]"/>
      <card class="col-4" :pokemonId="counter[4]"/>
      <card class="col-4" :pokemonId="counter[5]"/> -->
    </div>
  </main>
</template>

<style scoped>
.btn-left {
  position: fixed;
    top: 0;
    height: 50%;
    margin: auto 0;
    left: 0;
    bottom: 0;
}
.btn-right {
  position: fixed;
    top: 0;
    height: 50%;
    margin: auto 0;
    right: 0;
    bottom: 0;
}

</style>
