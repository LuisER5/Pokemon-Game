<template>
  <div class="container">
    <PokemonPage />
  </div>
</template>

<script>
import PokemonPage from "./pages/PokemonPage.vue";

export default {
  name: "App",
  components: {
    PokemonPage,
  },
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}

.container {
  height: 50%;
  margin-top: 40px;
  margin-right: auto;
  margin-left: auto;
  width: 50%;
}
</style>
