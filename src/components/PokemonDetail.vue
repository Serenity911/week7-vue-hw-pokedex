<template lang="html">
  <div class= "screen1">
    <h2>{{ selectedPkmn.name }}</h2>
    <p>{{ selectedPkmn.id }}</p>
    <p v-for='type in resultOfGetTypes'>{{ type }}</p>
  </div>
</template>

<script>
export default {
  name: 'pokemon-detail',
  props: ['selectedPkmn'],
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
    }
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
  background-color: grey;
  border: solid grey thin;
  height: 561px;
  justify-content: space-evenly;
  align-items: center;
}
</style>
