<template>
  <div id="app">
    <pokemon-list :pokemons="pokemons"></pokemon-list>
  </div>
</template>

<script>
import PokemonList from './components/PokemonList';

function fetchPokemons() {
  return fetch('../static/mock-data/pokemons.json')
    .then((response) => {
      return response.json();
    });
}

export default {
  data () {
    return {
      pokemons: []
    }
  },
  created () {
    fetchPokemons().then((response) => {
      this.pokemons = response.results;
    });
  },
  components: {
    PokemonList
  }
}
</script>

<style>

</style>
