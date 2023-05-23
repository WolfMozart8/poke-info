<template>
    <div v-if="pokemon" class="pokemon-card" :style="{'background-color':info.color.name}">
        <div class="img-container">
            <img class="pokemon-image" :src="pokemon.sprites.front_default" alt="Pokemon image">
        </div>
        <h2 v-if="info" class="pokemon-name-jp">{{ info.names[0].name }}</h2>
        <div class="pokemon-info">
            <div class="pokemon-info-name">
                <h2 class="pokemon-name">{{ pokemon.name.toUpperCase() }}</h2>
            </div>
            <div class="pokemon-info-body">
                <div class="kilos">
                    <div>
                        {{ numberFormat(pokemon.weight) }}
                    </div>
                    <div>
                        KG
                    </div>
                </div>
                <div class="height">
                    <div>
                        {{ numberFormat(pokemon.height) }}
                    </div>
                    <div>
                        M
                    </div>
                </div>
            </div>
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
import { ref, watchEffect, onActivated, onDeactivated } from 'vue';
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
    onActivated(() => {
  // called on initial mount
  // and every time it is re-inserted from the cache
})

onDeactivated(() => {
  // called when removed from the DOM into the cache
  // and also when unmounted
})
const numberFormat = (num) => {
    if (num < 10) {
        return "0." + num;
    }
    else {
        const firstText = num.toString().slice(0, -1);
        const secondText = num.toString().slice(-1);
        return firstText.concat(".", secondText)

    }
}
    const fetchPokemon = async ()=> {
        const responsePokemon = await fetch(`https://pokeapi.co/api/v2/pokemon/${props.pokemonId}`);
    };
</script>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=DotGothic16&display=swap');

.loading-div {
    width: 300px;
    height: 300px;
}
.img-container {
    width: 100%;
    background: url(../../src/assets/img/bg-grass.png);
    background-size: cover;
    border-radius: 10px 10px 0 0;



}
.pokemon-info {
    grid-column: 1 / 2;
    grid-row: 2 / 3;
    background-color: #F8F8F8;
    border-radius: 0 0 10px 10px;
}
.pokemon-info-body {
    display: flex;
    font-size: 1.5em;
    justify-content: space-around;
    align-items: center;
    height: 80%;
}
.pokemon-name-jp {
    font-family: 'DotGothic16', sans-serif;
    color: #ccc;
    /* position: absolute; */
    writing-mode: tb;
    /* top: 20px;
    right: 0px; */
    grid-column: 2 / 3;
    grid-row: 1 / 3;
}

.pokemon-card {
    width: 300px;
    height: 300px;
    border: 1px solid #ccc;
    border-radius: 10px;
    padding: 10px;
    /* display: flex;
    flex-direction: column;
    align-items: center; */
    display: grid;
    grid-template-columns: 3fr 1fr;
    grid-template-rows: 1fr 1fr;

    text-align: center;
    /* position: relative; */
    background-color: #F8F8F8;
}

.pokemon-image {
    width: 150px;
    height: auto;
    object-fit: cover;
    margin-bottom: 10px;

    grid-column: 1 / 2;
    grid-row: 1 / 2;
}

/* .pokemon-info {
    flex-grow: 1;
} */

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