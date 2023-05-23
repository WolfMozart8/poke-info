<template>
    <div v-if="pokemon && info" class="pokemon-card" :class="info.color.name">
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
import { ref, watchEffect } from 'vue';
    const pokemon = ref(null);
    const info = ref(null);
    let colors = [
    "green", 
    "red",
    "blue",
    "white",
    "brown",
    "yellow",
    "purple",
    "pink",
    "gray",
    "black"
]

    const props = defineProps({
        pokemonId: Number
    });
    watchEffect(async () => {
        const url = `https://pokeapi.co/api/v2/pokemon/${props.pokemonId}`;
        const urlInfo = `https://pokeapi.co/api/v2/pokemon-species/${props.pokemonId}/`;
        pokemon.value = await ((await fetch(url)).json());
        info.value = await((await fetch(urlInfo)).json());
    });

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
    border: none;
    background-color: #F8F8F8;

    box-shadow: 0px 10px 22px 3px rgba(0,0,0,0.1);
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
/* cards colors */
.green {
    background: rgb(11,104,26);
background: linear-gradient(90deg, rgba(11,104,26,1) 6%, rgba(64,155,13,1) 52%, rgba(62,140,12,1) 81%, rgba(26,85,8,1) 100%);
}
.red {
    background: rgb(104,11,11);
background: linear-gradient(90deg, rgba(104,11,11,1) 6%, rgba(155,13,13,1) 52%, rgba(140,12,12,1) 81%, rgba(85,8,8,1) 100%);
}
.blue {
    background: rgb(11,41,104);
background: linear-gradient(90deg, rgba(11,41,104,1) 6%, rgba(13,54,155,1) 52%, rgba(12,51,140,1) 81%, rgba(8,30,85,1) 100%);
}
.blue .pokemon-name-jp {
    color: #ccc;
}
.white {
    background: rgb(198,203,207);
background: linear-gradient(90deg, rgba(198,203,207,1) 6%, rgba(176,177,180,1) 52%, rgba(205,217,246,1) 81%, rgba(166,166,167,1) 100%);
}
.white .pokemon-name-jp {
    color: #333333;

}
.brown {
    background: rgb(145,107,35);
background: linear-gradient(90deg, rgba(145,107,35,1) 6%, rgba(213,159,58,1) 52%, rgba(209,144,45,1) 81%, rgba(127,97,14,1) 100%);
}
.brown .pokemon-name-jp {
    color: #333333;
}
.yellow {
    background: rgb(145,134,35);
background: linear-gradient(90deg, rgba(145,134,35,1) 6%, rgba(209,213,58,1) 52%, rgba(209,196,45,1) 81%, rgba(127,109,14,1) 100%);
}
.yellow .pokemon-name-jp {
    color: #333333;
}
.purple {
    background: rgb(84,23,122);
background: linear-gradient(90deg, rgba(84,23,122,1) 6%, rgba(154,58,213,1) 52%, rgba(144,45,209,1) 81%, rgba(80,14,127,1) 100%);
}
.pink {
    background: rgb(122,23,102);
background: linear-gradient(90deg, rgba(122,23,102,1) 6%, rgba(213,58,178,1) 52%, rgba(209,45,156,1) 81%, rgba(127,14,117,1) 100%);
}
.gray {
    background: rgb(139,139,139);
background: linear-gradient(90deg, rgba(139,139,139,1) 6%, rgba(203,193,200,1) 52%, rgba(204,188,198,1) 81%, rgba(165,165,165,1) 100%);
}
.gray .pokemon-name-jp {
    color: #333333;
}
.black {
    background: rgb(0,0,0);
background: linear-gradient(90deg, rgba(0,0,0,1) 6%, rgba(60,57,59,1) 52%, rgba(59,59,59,1) 81%, rgba(0,0,0,1) 100%);
}
</style>