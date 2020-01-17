<template lang="html">
  <div>
    <ul>
      <li v-for="(pokemon, index) in pokemonNameUrl" v-on:click="handleSelection(pokemon.name)"> {{ pokemon.name }} </li>
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
      selectedPkmnName: this.parentSelectedPkmnName
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
