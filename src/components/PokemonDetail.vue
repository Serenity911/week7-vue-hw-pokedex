<template lang="html">
  <div>
    <h2>{{ selectedPkmn.name }}</h2>
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
  // mounted() {
  //   this.getTypes()
  // },
  methods: {
    getTypes() {
      // this.$nextTick(function () {
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
</style>
