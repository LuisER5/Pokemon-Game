<template>
  <div class="pokemon-container" v-if="!pokemon">
    <h1 class="title">Espere por favor....</h1>
    <Spinner />
  </div>

  <div v-else class="pokemon-container">
    <h1 class="title">¿Quién es este Pokémon?</h1>
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
    <PokemonOptions :pokemons="pokemonsArr" @selection="checkAnswer($event)" />

    <template v-if="showAnswer">
      <h2>{{ message }}</h2>
    </template>
      <button class="reset-button" @click="newGame">Nuevo Juego</button>
  </div>
</template>

<script>
import PokemonPicture from "@/components/PokemonPicture.vue";
import PokemonOptions from "@/components/PokemonOptions.vue";
import Spinner from "@/components/Spinner.vue";

import getPokemonOptions from "@/helpers/getPokemonOptions";

export default {
  name: "PokemonPage",
  components: {
    PokemonPicture,
    PokemonOptions,
    Spinner
  },
  data() {
    return {
      pokemonsArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
    };
  },
  methods: {
    async mixPokemonsArray() {
      this.pokemonsArr = await getPokemonOptions();

      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonsArr[rndInt];
    },
    checkAnswer(selectedId) {
      this.showPokemon = true;
      this.showAnswer = true;

      this.message =
        selectedId === this.pokemon.id
          ? `Correcto, ${this.pokemon.name}`
          : `Oops, era ${this.pokemon.name}`;
    },
    newGame() {
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemonsArr = [];
      this.pokemon = null;
      this.mixPokemonsArray();
    },
  },
  mounted() {
    this.mixPokemonsArray();
  },
};
</script>

<style scoped>
.pokemon-container {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin-left: auto;
  margin-right: auto;
}
.title {
    padding-bottom: 10px;
}
.reset-button {
  margin-top: 10px;
  margin-bottom: 10px;
  padding: 10px 15px;
  cursor: pointer;
}
</style>