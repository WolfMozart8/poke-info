<script>
export default {
    data() {
        return {
            msg: "message here",
            pokemon: null,
        }
    },
    methods: {
        async fetchPokemon() {
            try {
                const response = await fetch(`https://pokeapi.co/api/v2/pokemon/squirtle`);

                if (!response.ok) {
                    throw new Error('No se pudo obtener el Pokémon.');
                }

                const data = await response.json();
                console.log(data)
                this.pokemon = data
            } catch (error) {
                console.log(error);
            }
        }
    }
}
</script>

<template>
    <h1>{{ msg }}</h1>
    <button @click="fetchPokemon">Obtener Pokémon</button>
    <div v-if="pokemon" class="pokemon-card">
        <img class="pokemon-image" :src="pokemon.sprites.front_default" alt="Imagen del Pokémon">
        <div class="pokemon-info">
            <h2 class="pokemon-name">{{ pokemon.name }}</h2>
            <p class="pokemon-id">ID: {{ pokemon.id }}</p>
        </div>
    </div>
</template>

<style>
.pokemon-card {
    width: 300px;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 10px;
    display: flex;
    align-items: center;
}

.pokemon-image {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    object-fit: cover;
    margin-right: 10px;
}

.pokemon-info {
    flex-grow: 1;
}

.pokemon-name {
    font-size: 20px;
    margin: 0;
}

.pokemon-id {
    font-size: 14px;
    margin: 5px 0;
}
</style>