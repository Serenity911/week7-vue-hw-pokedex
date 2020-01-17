<template lang="html">
  <div>
    <pokemon-list :pokemonNameUrl='pokemonNameUrl'/>
  </div>
</template>

<script>
import PokemonList from './components/PokemonList.vue'

export default {
  name: 'app',
  data() {
    return {
      pokemonNameUrl: [],
      parentSelectedPkmnName: 'bulbasaur'
    }
  },
  mounted() {
    this.fetchPomekonNames()
  },
  methods: {
    fetchPomekonNames() {
      fetch('https://pokeapi.co/api/v2/pokemon/?limit=808')
      .then(result => result.json())
      .then(result => this.pokemonNameUrl = result.results )
    }
  },
  components: {
    "pokemon-list": PokemonList
  }
}
</script>

<style lang="css">

</style>
