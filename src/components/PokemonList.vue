<template lang="html">
  <div>
    <ul>
      <li v-for="pokemon in pokemonNameUrl" :key="pokemon.name">{{ pokemon.name }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'pokemon-list',
  props: ['pokemonNameUrl', 'parentSelectedPkmnName'],
  data() {
    return {
      selectedPkmnName: this.parentSelectedPkmnName
    }
  }
}
</script>

<style lang="css" scoped>
</style>
