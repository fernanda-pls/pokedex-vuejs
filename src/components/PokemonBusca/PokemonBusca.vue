<template>
  <form>
    <input
      name="busca"
      id="busca"
      type="text"
      placeholder="Search"
      @input="setValue($event.target.value)"
    >
  </form>
</template>

<script>
export default {
  name: "PokemonBusca",
  props: {
    searchValue: {
      type: String
    }
  },
  methods: {
    setValue(searchValue) {
      this.$emit("toFilter", searchValue);
    }
  }
};
</script>

<style src="./busca.scss" lang="scss" scoped/>
