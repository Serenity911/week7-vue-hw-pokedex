<template lang="html">
  <div>
    <h2>{{ selectedPkmn.name }}</h2>
    <!-- add another section as the selectedpkmn returns id and name immediately, but takes two calls to get the type and returns an empty p if no workaround  -->
    <p >{{ resultOfGetTypes }}</p>
  </div>
</template>

<script>
export default {
  name: 'pokemon-detail',
  props: ['selectedPkmn'],
  // data(){
  //   return {
  //     resultOfGetTypes: null
  //   }

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

        let selectedNameTypeZero = selectedPkmnTypes[0].type.name
        console.log(selectedNameTypeZero)
        return selectedNameTypeZero
      // })
    }
  }
}

</script>

<style lang="css" scoped>
</style>
