<template lang="html">
  <div class= "screen1">
    <div class="button-placeholder" v-on:click="getList">X</div>
    <div class="info" v-if="showGeneralInfo">
      <!-- why I need to have selectedPkmn as the first one? if it renders and finds undefined because it hasn't loaded everything yet, it fails the v-if in the app? -->
      <h1>{{ selectedPkmn.name }}</h1>
      <img :src="resultOfGetImg">
      <!-- get type  -->
      <div class="horizontal-list">
        <p v-for='type in resultOfGetTypes'>{{ type }}</p>
      </div>
    </div>

    <!-- get moves -->
    <div class="moves" v-if="showMoves">
      <ul id="scrollable-list">
        <li v-for='move in resultOfGetMoves'>{{ move }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name: 'pokemon-detail',
  props: ['selectedPkmn', 'section'],
  data() {
    return {
      showGeneralInfo: true,
      showMoves: false
    }
  },
  computed: {
    resultOfGetTypes: function() {
      return  this.getTypes()
    },
    resultOfGetImg: function() {
      let selectedPkmnSprites = this.selectedPkmn.sprites
      if (!selectedPkmnSprites) return "";
      console.log("how many sprites", selectedPkmnSprites);
      return this.selectedPkmn.sprites.front_default
    },
    resultOfGetAbilities: function() {
      return this.getAbilities()
    },
    resultOfGetMoves: function() {
      return this.getMoves()
    },
    showSection: function() {
      this.section === 'info' ? this.showGeneralInfo = true : this.showGeneralInfo = false

    }
  },
  methods: {
    getTypes() {
      let selectedPkmnTypes = this.selectedPkmn.types
      if (!selectedPkmnTypes) return
      let selectedNameType = []
      selectedPkmnTypes.forEach(el => selectedNameType.push(el.type.name))
      return selectedNameType
    },
    getImg() {

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
    display: grid;
    grid-template-columns: 20% 20% 20% 20% 20%;
    grid-template-rows: 5% 85% 10%;
    grid-template-areas:
    "button1 . . . ."
    " . title title title ."
    " .  . type . .";
    /* grid-template:
    [row1-start] "button1 . . . . ." 20px [row1-end]
    [row1-start] "title title title" 25px [row1-end] */

    background-color: rgb(186, 186, 186);
    border: solid grey thin;
    height: 561px;
    justify-content: center;

  }
  h1 {


  }
  .moves{
    grid-area: moves;
    /* grid-row: 5/5; */


  }
  #scrollable-list {
    /* overflow: auto;
    list-style: none;
    padding: 0;
    display: grid;
    grid-template-columns: 40% 40% 40%; */
  }

  .button-placeholder {
    grid-area: button1;
    grid-row: 1/3;
    /* border-radius: 0.6em;
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
    align-self: flex-start; */
  }
  .button-placeholder:hover {
    background-color: rgb(149, 149, 149);
    border-color: rgb(216, 216, 216) rgb(209, 209, 209) rgb(148, 146, 146);
  }

  .info {
    grid-area: title;
    grid-row: 2/3;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    /* display: grid;
    grid-template-columns: 50% 50%;
    align-items: center; */
  }

  .horizontal-list {
    grid-area: type;
    /* grid-row: 3/3; */

    display: flex;
    width: 100%;
    justify-content: space-evenly;
    /* display: grid;
    grid-template-columns: 50px 50px;
    justify-content: center;
    list-style: none; */
  }

  img {
    /* grid-area: img; */
    /* grid-row: 3/5; */
    width: 155%;
    flex-shrink: 0;
    height: auto;
  }

</style>
