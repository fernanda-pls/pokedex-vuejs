<template>
  <div id="app">
    <PokemonApp/>
  </div>
</template>

<script>
import PokemonApp from "./components/PokemonApp/PokemonApp";

export default {
  name: "App",
  components: {
    PokemonApp
  }
};
</script>

<style src="./assets/scss/_global.scss" lang="scss"/>
