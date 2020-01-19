<template lang="html">
  <div class= "screen1">
    <div class="button-placeholder" v-on:click="getList">X</div>
    <div class="info">
      <!-- why I need to have selectedPkmn as the first one? if it renders and finds undefined because it hasn't loaded everything yet, it fails the v-if in the app? -->
      <h2>{{ selectedPkmn.name }}</h2>
      <img :src="resultOfGetImg" alt>
      <div class="horizontal-list">
        <p v-for='type in resultOfGetTypes'>{{ type }}</p>
      </div>
    </div>

    <ul id="scrollable-list">
      <li v-for='move in resultOfGetMoves'>{{ move }}</li>
    </ul>
  </div>
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name: 'pokemon-detail',
  props: ['selectedPkmn', 'moves'],
  computed: {
    resultOfGetTypes: {
      get: function() {
        return  this.getTypes()
      }
    },
    resultOfGetImg: {
      get: function() {
        return this.getImg()
      }
    },
    resultOfGetAbilities: {
      get: function() {
        return this.getAbilities()
      }
    },
    resultOfGetMoves: {
      get: function() {
        return this.getMoves()
      }
    }
  },
  methods: {
    getTypes() {
      // console.log("get types")
      let selectedPkmnTypes = this.selectedPkmn.types
      if (!selectedPkmnTypes) return
      let selectedNameTypeZero = []
      selectedPkmnTypes.forEach(el => selectedNameTypeZero.push(el.type.name))
      return selectedNameTypeZero
    },
    getImg() {
      let selectedPkmnSprites = this.selectedPkmn.sprites
      console.log("how many sprites", selectedPkmnSprites);
      return this.selectedPkmn.sprites.front_default
    },
    getAbilities() {
      let selectedPkmnAbilities = this.selectedPkmn.abilities
      // console.log(selectedPkmnAbilities);
      let selectedPkmnAbilitiesNames = []
      selectedPkmnAbilities.forEach(el => selectedPkmnAbilitiesNames.push(el.ability.name))
      return selectedPkmnAbilitiesNames
    },
    getMoves() {
      let selectedPkmnMoves = this.selectedPkmn.moves
      console.log(selectedPkmnMoves);
      let selectedPkmnMovesNames = []
      selectedPkmnMoves.forEach(el => selectedPkmnMovesNames.push(el.move.name))
      return selectedPkmnMovesNames
    },
    getList() {
      eventBus.$emit('home-requested', "home")

    },
    showMoves(){

    }
    // question: why is it calling every function twice? is it because: it renders, the function takes a bit to be processed and returns undefined and I have to call them in computed properties to have them re-evaluated once everything is loaded?
    // getName() {
    //   let namegetname = this.selectedPkmn.sprites
    //   console.log("how many times get name", namegetname);
    //   return namegetname
    // }
  }
}

</script>

<style lang="css" scoped>
.screen1 {
  display: flex;
  flex-direction: column;
  /* max-width: 30rem; */
  /* display: grid; */
  /* grid-template-columns: 10% 90%; */
  background-color: rgb(186, 186, 186);
  border: solid grey thin;
  height: 561px;
  justify-content: space-evenly;
  align-items: center;
}
#scrollable-list {
  overflow: auto;
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: 40% 40% 40%;
}

.button-placeholder {
  border-radius: 0.6em;
  display: inline-block;
  align-items: flex-start;
  background-color: rgb(186, 186, 186);
  box-sizing: border-box;
  margin: 0.5em;
  padding: 1px 7px 2px;
  border-width: 1px;
  border-style: solid;
  border-color: rgb(216, 216, 216) rgb(209, 209, 209) rgb(186, 186, 186);
  flex-grow: 1;
  align-self: flex-start;
}
.info {
  display: grid;
  grid-template-columns: 50% 50%;
  align-items: center;
}

.horizontal-list {
  display: grid;
  grid-template-columns: 50px 50px;
  justify-content: center;
  list-style: none;
}


</style>
