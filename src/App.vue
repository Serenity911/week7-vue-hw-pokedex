<template lang="html">
  <div>
    <pokemon-list :pokemonNameUrl='pokemonNameUrl' :parentSelectedPkmnName='selectedPkmnName'/>
  </div>
</template>

<script>
import PokemonList from './components/PokemonList.vue'
import { eventBus } from './main.js'

export default {
  name: 'app',
  data() {
    return {
      pokemonNameUrl: [],
      selectedPkmnName: 'bulbasaur'
    }
  },
  mounted() {
    this.fetchPomekonNames(),
    eventBus.$on('pokemon-selected', (nameSelected) => this.selectPokemon(nameSelected))
  },
  methods: {
    fetchPomekonNames() {
      fetch('https://pokeapi.co/api/v2/pokemon/?limit=808')
      .then(result => result.json())
      .then(result => this.pokemonNameUrl = result.results )
    },
    selectPokemon(nameSelected) {
      return this.selectedPkmnName = nameSelected
    }
  },
  components: {
    "pokemon-list": PokemonList
  }
}
</script>

<style lang="css">

</style>
