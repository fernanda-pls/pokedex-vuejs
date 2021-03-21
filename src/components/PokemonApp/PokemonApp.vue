<template>
  <div>
    <PokemonBusca @toFilter="handleFilter" :searchValue="pokemonFiltro"/>
    <div v-if="pokemons && pokemons.length">
      <PokemonCard :pokemons="buscaPokemon" @clicked="handleDetalhes"/>
    </div>
    <div v-if="toggle">
      <PokemonModal :detalhesPokemon="detalhesPokemon" @clicked="fecharModal"/>
    </div>
  </div>
</template>

<script>
import PokemonBusca from "../PokemonBusca/PokemonBusca";
import PokemonCard from "../PokemonCard/PokemonCard";
import PokemonModal from "../PokemonModal/PokemonModal";

export default {
  name: "PokemonApp",
  data() {
    return {
      pokemons: [],
      pokemonFiltro: "",
      pokemonId: "1",
      toggle: false,
      detalhesPokemon: null
    };
  },
  components: {
    PokemonBusca,
    PokemonCard,
    PokemonModal
  },
  computed: {
    buscaPokemon() {
      if (this.pokemonFiltro === "" || this.pokemonFiltro === " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter(pokemon =>
          pokemon.name.toLowerCase().match(this.pokemonFiltro.toLowerCase())
        );
      }
    }
  },
  methods: {
    getPokemon() {
      fetch("https://pokeapi.co/api/v2/pokemon?limit=151")
        .then(response => response.json())
        .then(response => {
          const resultado = response.results.map((item, i) => {
            let pokemon = {
              id: i + 1,
              name: item.name[0].toUpperCase() + item.name.substr(1),
              img: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${i +
                1}.png`
            };
            return pokemon;
          });
          this.pokemons = resultado;
        });
    },
    handleFilter(pokemonFiltro) {
      this.pokemonFiltro = pokemonFiltro;
    },
    handleDetalhes(detalhesPokemon) {
      this.detalhesPokemon = detalhesPokemon;
      this.toggle = true;
    },
    fecharModal() {
      this.toggle = false;
    }
  },
  created() {
    this.getPokemon();
  }
};
</script>
