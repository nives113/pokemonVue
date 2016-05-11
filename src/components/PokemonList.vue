<template>
  <div class="left">
    <input type="text" v-model="findPokemon" debounce="500" placeholder="Search"/>
    <ul>
      <li v-for="pokemon in pokemons | filterBy findPokemon" @click="selectPokemon(pokemon.url)">
        {{pokemon.name}}
      </li>
    </ul>
  </div>
  <div class="right">
    <div v-if="pokemonInfo.name"><h2>Pokemon Info</h2></div>
    <div v-if="pokemonInfo.name">Name: {{pokemonInfo.name}}</div>
    <div v-if="pokemonInfo.height">Height: {{pokemonInfo.height}}</div>
    <div v-if="pokemonInfo.weight">Weight: {{pokemonInfo.weight}}</div>
    <div v-if="pokemonInfo.abilities.length !== 0">Abilities number: {{pokemonInfo.abilities.length}}</div>
  </div>
</template>

<script>
function fetchPokemon(url) {
  return fetch(url)
    .then((response) => {
      return response.json();
    });
}

export default {
  props: ['pokemons'],
  data () {
    return {
      pokemonInfo: {
        name: '',
        height: '',
        weight: '',
        abilities: []
      }
    }
  },
  methods: {
    selectPokemon(url) {
      fetchPokemon(url).then((response) => {
        this.pokemonInfo = response;
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  ul {
    list-style: none;
    color: red;
  }
  li {
    margin-top: 10px;
  }
  .left {
    width: 50%;
    float: left;
    font-size: 2em;
  }
  .right {
    width: 50%;
    float: right;
    font-size: 2em;
  }
  input {
    height: 40px;
    border-radius: 3px;
    border: solid;
    padding-left: 10px;
    font-size: 1.2em;
  }
</style>
