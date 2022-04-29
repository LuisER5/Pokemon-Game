<template>
  <div class="pokemon-container">
    <img 
        class="hidden-pokemon" 
        :src="imgSrc" 
        alt="pokemon"/>
    <img v-if="showPokemon"
        class="fade-in" 
        :src="imgSrc" 
        alt="pokemon"/>
  </div>
</template>

<script>
export default {
  props: {
    pokemonId: {
      type: Number,
      required: true,
      default: 1,
    },
    showPokemon: {
        type: Boolean,
        required: true,
        default: false
    }
  },
  computed: {
    imgSrc() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
    },
  },
};
</script>

<style scoped>
/* Pokemon Picture */
.pokemon-container {
  position: relative;
  height: 250px;
  width: 100%;
}
img {
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
  height: 200px;
  left: 0;
  margin: auto;
  position: absolute;
  right: 0;
  user-select: none;
}
.hidden-pokemon {
  filter: brightness(0);
}
</style>