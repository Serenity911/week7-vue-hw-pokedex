<template lang="html">
  <div>
    <ul>
      <li v-if="pokemon" v-for="pokemon in getTwentyItems" v-on:click="handleSelection(pokemon.name)"> {{ pokemon.name }} </li>
    </ul>
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
    }
  }
}
</script>

<style lang="css" scoped>
</style>
