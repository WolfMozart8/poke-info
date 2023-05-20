<template>
    <div v-if="pokemon" class="pokemon-card">
        <img class="pokemon-image" :src="pokemon.sprites.front_default" alt="Pokemon image">
        <div class="pokemon-info">
            <h2 class="pokemon-name">{{ pokemon.name.toUpperCase() }}</h2>
            <h2 v-if="info" class="pokemon-name-jp">{{ info.names[0].name }}</h2>
            <!-- <p class="pokemon-id">ID: {{ pokemon.id }}</p> -->
            <!-- <p v-if="info" class="pokemon-description">{{ info.flavor_text_entries[0].flavor_text }}</p> -->
        </div>
    </div>
    <div class="loading-div" v-else>
        <div class="spinner-border loading" role="status">
            <span class="visually-hidden">Loading...</span>
        </div>
    </div>
</template>

<script setup>
import { ref, watchEffect } from 'vue';
    const pokemon = ref(null);
    const info = ref(null);

    const props = defineProps({
        pokemonId: Number
    });
    watchEffect(async () => {
        const url = `https://pokeapi.co/api/v2/pokemon/${props.pokemonId}`;
        const urlInfo = `https://pokeapi.co/api/v2/pokemon-species/${props.pokemonId}/`;
        pokemon.value = await ((await fetch(url)).json());
        info.value = await((await fetch(urlInfo)).json());
    });
    const fetchPokemon = async ()=> {
        const responsePokemon = await fetch(`https://pokeapi.co/api/v2/pokemon/${props.pokemonId}`);
    };
</script>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=Rampart+One&display=swap');

.loading-div {
    width: 300px;
    height: 300px;
}

.pokemon-name-jp {
    font-family: 'Rampart One', cursive;
    position: absolute;
    writing-mode: tb;
    top: 20px;
    right: 0px;
}

.pokemon-card {
    width: 300px;
    height: 300px;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    position: relative;
    background-color: #F8F8F8;
}

.pokemon-image {
    width: 150px;
    height: auto;
    border-radius: 10px;
    object-fit: cover;
    margin-bottom: 10px;
    background: url(../../src/assets/img/bg-grass.png);
    background-size: cover;
}

.pokemon-info {
    flex-grow: 1;
}

.pokemon-name {
    font-size: 20px;
    margin: 0;
    color: #333333;
}

.pokemon-id {
    font-size: 14px;
    margin: 5px 0;
    color: #666666;
}

.pokemon-description {
    font-size: 14px;
    margin: 10px 0;
    color: #888888;

}
</style>