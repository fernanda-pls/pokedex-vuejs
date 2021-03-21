<template>
  <section class="modal-container">
    <div class="modal">
      <button @click="fecharModal">X</button>
      <div class="infos">
        <h2>{{detalhesPokemon.name}}</h2>
        <p>Habilidade: {{detalhesPokemon.abilities}}</p>
        <p>Peso: {{detalhesPokemon.weight}}</p>
        <p>Altura: {{detalhesPokemon.height}}</p>
      </div>
      <img id="imgf" :src="detalhesPokemon.imgFront" alt="Pokemon Frente">
      <img id="imgb" :src="detalhesPokemon.imgBack" alt="Pokemon Costas">
    </div>
  </section>
</template>

<script>
export default {
  name: "PokemonModal",
  props: {
    detalhesPokemon: {
      type: Object
    }
  },
  methods: {
    fecharModal() {
      this.$emit("clicked", this.fecharModal);
    }
  }
};
</script>

<style src="./modal.scss" lang="scss" scoped/>
