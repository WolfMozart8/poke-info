<script>
export default {
    data() {
        return {
            info: null,
            pokemon: null,
        }
    },
    props : {
        pokemonId : Number
    },
    
    methods: {
        async fetchPokemon() {
            console.log(this.pokemonId)
            try {
                const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokemonId}`);

                if (!response.ok) {
                    throw new Error('No se pudo obtener el Pokémon.');
                }

                const data = await response.json();
                console.log(data)
                this.pokemon = data
                
                const responseInfo = await fetch(`https://pokeapi.co/api/v2/pokemon-species/${this.pokemonId}/`)

                if (!responseInfo.ok) {
                    throw new Error('No se pudo obtener el Pokémon.');
                }

                const dataInfo = await responseInfo.json();
                this.info = dataInfo

                console.log(this.info)
            } catch (error) {
                console.log(error);
            }
        }
    },
    // async fetchInfo(pokemon) {
    //     try {
    //         const response = await fetch(`https://pokeapi.co/api/v2/pokemon-species/${pokemon}/`)

    //         if (!response.ok) {
    //                 throw new Error('No se pudo obtener el Pokémon.');
    //             }
    //         const data = await response.json();

    //         this.info = data
    //     } catch (error) {
    //         console.log(error)
    //     }
    // }
}
</script>

<template>
    <button @click="fetchPokemon">Obtener Pokémon</button>
    <div v-if="pokemon" class="pokemon-card">
        <img class="pokemon-image" :src="pokemon.sprites.front_default" alt="Imagen del Pokémon">
        <div class="pokemon-info">
            <h2 class="pokemon-name">{{ pokemon.name }}</h2>
            <h2 v-if="info" class="pokemon-name-jp">{{ info.names[0].name }}</h2>
            <p class="pokemon-id">ID: {{ pokemon.id }}</p>
            <p v-if="info" class="pokemon-description">{{ info.flavor_text_entries[0].flavor_text }}</p>
        </div>
    </div>
    <div v-else>...loading</div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Rampart+One&display=swap');

.pokemon-name-jp {
    font-family: 'Rampart One', cursive;
    position: absolute;
    writing-mode: tb;
    top: 20px;
    right: 0px;
}
.pokemon-card {
    width: 300px;
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