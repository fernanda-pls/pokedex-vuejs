<template>
  <div class="pokemons">
    <div
      class="pokemon"
      v-for="pokemon in pokemons"
      :key="pokemon.id"
      @click="handleClick(pokemon.id)"
    >
      <img class="pokemon-img" :src="pokemon.img" alt="Imagem Pokemon">
      <p class="pokemon-detalhes">
        <span>{{pokemon.name}}</span>
        <span>#{{pokemon.id}}</span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonCard",
  props: {
    pokemons: {
      type: Array
    }
  },
  data() {
    return {
      detalhesPokemon: {
        id: null,
        name: null,
        weight: null,
        height: null,
        imgFront: null,
        imgBack: null,
        abilities: null
      }
    };
  },
  methods: {
    handleClick(pokemonId) {
      fetch(`http://pokeapi.co/api/v2/pokemon/${pokemonId}`)
        .then(response => response.json())
        .then(response => {
          this.detalhesPokemon.id = response.id;
          this.detalhesPokemon.name =
            response.forms[0].name[0].toUpperCase() +
            response.forms[0].name.substr(1);
          this.detalhesPokemon.weight = response.weight;
          this.detalhesPokemon.height = response.height;
          (this.detalhesPokemon.imgFront = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
            response.id
          }.png`),
            (this.detalhesPokemon.imgBack = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/${
              response.id
            }.png`);
          this.detalhesPokemon.abilities = response.abilities[0].ability.name;
        });

      this.$emit("clicked", this.detalhesPokemon);
    }
  }
};
</script>

<style src="./card.scss" lang="scss" scoped/>
