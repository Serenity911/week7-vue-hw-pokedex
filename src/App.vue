<template lang="html">
  <div id="page-container">

    <div class="pokedex">
      <div class="top-container">
        <div class="circled-button">
        </div>
        <div class="trio">
          <div class="mini-circle">
          </div>
          <div class="mini-circle">
          </div>
          <div class="mini-circle">
          </div>
        </div>
      </div>

      <div class="middle-container">
        <pokemon-list  :pokemonNameUrl='pokemonNameUrl' :parentSelectedPkmnName='selectedPkmnName'/>
        <!-- <pokemon-detail :class='displayDetail' v-if='selectedPkmn' :selectedPkmn='selectedPkmn' /> -->
      </div>

    </div>
    <div class="pokedex">
      <div class="right-screen">
        <pokemon-detail  v-if='selectedPkmn' :selectedPkmn='selectedPkmn' :section='section' />
        <!-- <button v-on:click="showMoves">Moves</button> -->
      </div>

      <div class="poke-end">
        <div class="buttons">
          <button v-on:click="section = 'moves' ">Moves</button>
          <button></button>
          <button></button>
          <button></button>
          <button></button>
          <button></button>
          <button></button>
          <button></button>
          <button></button>
          <button></button>

        </div>
        <div class="medium-circled-button">
        </div>
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
      selectedPkmn: null,
      typedName: "",
      section: "info"
    }
  },
  mounted() {
    this.fetchPomekonNames(),
    eventBus.$on('pokemon-selected', (nameSelected) => this.selectPokemon(nameSelected))
    eventBus.$on('home-requested', () => this.handleHomeRequested())
    eventBus.$on('pokemon-typed', (typedName) => this.searchPkmn(typedName) )
  },
  // computed: {
    // displayDetail: function () {
    //   return this.selectedPkmn ? "toggleOn" : "toggleOff"
    // },
    // displayList: function () {
    //   return this.selectedPkmn ? "toggleOff" : "toggleOn"
    // }

  // },
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
      // console.log("how many times in select Pokemon", nameSelected);
      // this.selectedPkmnName = nameSelected
      let findPokemonNameUrl = this.findPokemon(nameSelected)
      fetch(findPokemonNameUrl.url)
      .then(result => result.json())
      .then(result => this.selectedPkmn = result )
    },
    showMoves() {
      this.moves = "yes"
    },
    searchPkmn(typedName) {
        // console.log("selected pkmn before search", typedName);
        this.typedName = typedName
        let mappedNames = this.pokemonNameUrl.map(el => el.name.toLowerCase())
        // console.log("mapped Names", mappedNames)
        let pokemonTyped = mappedNames.find(pokemon => pokemon.startsWith(this.typedName))
        // console.log("selected pkmn middle search", pokemonTyped);
        // this.selectedPkmnName = pokemonTyped
        return this.selectPokemon(pokemonTyped)
        // console.log("selected pkmn after search", selectedPkmn);
      },
    handleHomeRequested() {
        this.selectedPkmn = null
        this.section = "info"
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
  justify-content: center;
}
.pokedex {
  border: solid red thin;
  border-radius: 2em;
  background-color: red;
  padding: 1em 5em;
  max-width: 30rem;
  align-self: center;
  flex-grow: 1;
  margin-top: 1rem;
  height: 800px;
}
.pokedex:last-of-type {
  height: 700px;
  align-self: flex-end;
}

.toggleOn {
}

.toggleOff {
  display: none;
}

.circled-button {
  width: 70px;
  height: 70px;
  background-color: rgb(133, 193, 236);
  border-radius: 100%;
  margin: 3%;
  border: 0.1em solid rgba(213, 238, 247, 0.87);
}
.medium-circled-button {
  width: 50px;
  height: 50px;
  background-color: black;
  border-radius: 100%;
  margin: 3%;

}

.trio {
  padding-left: 10%;
  display: flex;
  padding-top: 3%;

}
/* rendering gets a bit randomic, ask why? */
.mini-circle {
  width: 20px;
  height: 20px;
  border-radius: 100%;
  background-color: rgb(198, 0, 0);
  margin-right: 5px;
}

.mini-circle:nth-child(2) {
  background-color: rgb(255, 227, 79);
}
.mini-circle:last-child {
  background-color: rgb(32, 210, 49)
}

.top-container {
  display: flex;
  flex-direction: row;
  border-bottom: solid darkred 10px;

}

.middle-container {
  border-top: crimson solid 10px;
  margin-top: 0;
}



.right-screen {
  background-color: grey;
  border: solid grey thin;
  height: 561px;
  margin-top: 18px;
}

.buttons {
  display: grid;
  grid-template-columns: 20% 20% 20% 20% 20%;;
  grid-template-rows: auto;
}
.buttons button {
  background-color: rgb(62, 165, 231);
  height: 20px;
  border: solid thin rgb(159, 213, 251);

}
.poke-end {
  /* align-self:flex-end; */
  margin-top: 2px;

}

</style>
