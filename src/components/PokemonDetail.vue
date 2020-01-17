<template lang="html">
  <div>
    <h2>{{ selectedPkmn.name }}</h2>
    <p>{{ getTypes() }}</p>
  </div>
</template>

<script>
export default {
  name: 'pokemon-detail',
  props: ['selectedPkmn'],
  data(){
    return {
      resultOfGetTypes: null

    }
  },
  // mounted() {
  //   this.getTypes()
  // },
  methods: {
    getTypes() {
      console.log("get types")
      let selectedPkmnTypes = this.selectedPkmn.types
      if (!selectedPkmnTypes) return

      let selectedNameTypeZero = selectedPkmnTypes[0].type.name
      console.log(selectedNameTypeZero)
      return selectedNameTypeZero
    }
  }
}


</script>

<style lang="css" scoped>
</style>
