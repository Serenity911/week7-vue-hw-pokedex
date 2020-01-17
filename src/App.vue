<template lang="html">
  <div>
    <pokemon-list :pokemonNameUrl='pokemonNameUrl' :parentSelectedPkmnName='selectedPkmnName'/>
    <pokemon-detail v-if='selectedPkmn' :selectedPkmn='selectedPkmn' />
  </div>
</template>

<script>
import PokemonList from './components/PokemonList.vue'
import PokemonDetail from './components/PokemonDetail.vue'
import { eventBus } from './main.js'

export default {
  name: 'app',
  data() {
    return {
      pokemonNameUrl: [],
      selectedPkmnName: 'bulbasaur',
      selectedPkmn: null
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
    findPokemon(name) {
      return this.selectedPkmn = this.pokemonNameUrl.find(pokemon => pokemon.name === name)
    },
    selectPokemon(nameSelected) {
      console.log("how many times in select Pokemon", nameSelected);
      this.selectedPkmnName = nameSelected
      let findPokemonNameUrl = this.findPokemon(nameSelected)
      fetch(findPokemonNameUrl.url)
      .then(result => result.json())
      .then(result => this.selectedPkmn = result )
    }

  },
  components: {
    "pokemon-list": PokemonList,
    "pokemon-detail": PokemonDetail
  }
}
</script>

<style lang="css">

</style>
