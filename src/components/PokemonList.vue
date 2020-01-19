<template lang="html">
  <div>
    <div class="scroll-bar">
      <div class="button-placeholder" v-if="pageNumber === 1"></div>
      <button type="button" v-if="pageNumber !== 1" v-on:click="handlePreviousPage" v-model="pageNumber"> Previous </button>
      <button type="button" v-on:click="handleNextPage" v-model="pageNumber"> Next </button>
    </div>
    <div class="list">
      <ul>
        <li v-if="pokemon" v-for="pokemon in getTwentyItems" v-on:click="handleSelection(pokemon.name)"> {{ pokemon.name }} </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name: 'pokemon-list',
  props: ['pokemonNameUrl', 'parentSelectedPkmnName'],
  data() {
    return {
      selectedPkmnName: this.parentSelectedPkmnName,
      pageNumber: 1
    }
  },
  computed: {
    getTwentyItems: function() {
      let itemsPerPage = 20
      let lastItem = (itemsPerPage * this.pageNumber) - 1
      let firstItem = (this.pageNumber - 1) * itemsPerPage
      let twentyItemsNameUrl = []
      for (let i = firstItem; i < lastItem; i++) {
        console.log(this.pokemonNameUrl[i])
        twentyItemsNameUrl.push(this.pokemonNameUrl[i])
      }
      return twentyItemsNameUrl
    }
  },
  methods: {
    handleSelection(nameSelected) {
      this.selectedPkmnName = nameSelected
      eventBus.$emit('pokemon-selected', nameSelected )
    },
    handlePreviousPage() {
      this.pageNumber === 0 ? 0 : this.pageNumber -= 1
    },
    handleNextPage() {
      this.pageNumber += 1
    }
  }
}
</script>

<style lang="css" scoped>
.button-placeholder {
  border-radius: 0.1em;
  height:18px;
  width:39.125px;
  display: inline-block;
  align-items: flex-start;
  background-color: buttonface;
  box-sizing: border-box;
  margin: 0em;
  padding: 1px 7px 2px;
  border-width: 1px;
  border-style: solid;
  border-color: rgb(216, 216, 216) rgb(209, 209, 209) rgb(186, 186, 186);
}
</style>
