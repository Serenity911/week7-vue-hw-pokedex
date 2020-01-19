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
    }
  },
  methods: {
    getTypes() {
        console.log("get types")
        let selectedPkmnTypes = this.selectedPkmn.types
        if (!selectedPkmnTypes) return
        let selectedNameTypeZero = []
        selectedPkmnTypes.forEach(el => selectedNameTypeZero.push(el.type.name))
        return selectedNameTypeZero
      // })
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
