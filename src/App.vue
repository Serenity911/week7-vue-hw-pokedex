<template lang="html">
  <div id="page-container">
    <div class="pokedex">
      <div>
        <pokemon-list :class='displayList' :pokemonNameUrl='pokemonNameUrl' :parentSelectedPkmnName='selectedPkmnName'/>
        <pokemon-detail :class='displayDetail' v-if='selectedPkmn' :selectedPkmn='selectedPkmn' />
      </div>
      <div class="poke-end">
      </div>
    </div>
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
  computed: {
    displayDetail: function () {
      return this.selectedPkmn ? "toggleOn" : "toggleOff"
    },
    displayList: function () {
      return this.selectedPkmn ? "toggleOff" : "toggleOn"
    }
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

<style lang="css" scoped>
#page-container {
  display: flex;
  align-content: center;
}
.pokedex {
  border: solid red thin;
  border-radius: 2em;
  background-color: red;
  padding: 5em;
  max-width: 30rem;
  align-self: center;
  flex-grow: 1;
  margin-top: 1rem;
}

.toggleOn {
}

.toggleOff {
  display: none;
}
.poke-end {
  background-color: red;
  height: 10rem;
}

</style>
