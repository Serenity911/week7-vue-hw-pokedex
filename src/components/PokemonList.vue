<template lang="html">
  <div class= "screen">
    <div class="scroll-bar">
      <div class="button-placeholder" v-if="pageNumber === 1"></div>
      <button type="button" class="button-placeholder" v-if="pageNumber !== 1" v-on:click="handlePreviousPage" v-model="pageNumber"> Previous </button>
      <div class="button-bar"></div>
      <button type="button" class="button-placeholder" v-on:click="handleNextPage" v-model="pageNumber"> Next </button>
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
  border-radius: 0.6em 0.6em 0em 0;
  height:18px;
  width: 55.125px;
  display: inline-block;
  align-items: flex-start;
  background-color: rgb(186, 186, 186);
  box-sizing: border-box;
  margin: 0em;
  padding: 1px 7px 2px;
  border-width: 1px;
  border-style: solid;
  border-color: rgb(216, 216, 216) rgb(209, 209, 209) rgb(186, 186, 186);
  flex-grow: 1;

}

.button-placeholder:last-of-type {
  border-radius: 0em 0em 0.6em 0.6em;

}
.screen {
  /* display: flex;
  border: solid grey thin;
  border-radius: 0.5em;
  background-color: grey; */
  /* max-width: 30rem; */
  display: grid;
  grid-template-columns: 10% 90%;
  background-color: grey;
  border: solid grey thin;
}
.button-bar {
  flex-grow: 10;
  height:18px;
  width:39.125px;
  background-color: rgb(186, 186, 186);
  border-color: rgb(216, 216, 216) rgb(209, 209, 209) rgb(186, 186, 186);
  margin: 0em;
  padding: 1px 7px 2px;
  border-width: 1px;
  border-style: solid;
  background-color: rgb(186, 186, 186);
  border-color: rgb(216, 216, 216) rgb(209, 209, 209) rgb(186, 186, 186);
}

.scroll-bar {
  display: flex;
  flex-direction: column;
  justify-content: stretch;
  margin-right: 1rem;
  /* align-items: stretch;
}
.list {
/* width: 30rem; */
/* max-width: 30rem; */
/* set a width */
}

.list {
  margin-left: 0.5rem
}

ul {
  /* list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column; */
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  /* background-color: rgb(186, 186, 186);
  border-color: rgb(216, 216, 216) rgb(209, 209, 209) rgb(186, 186, 186);
  margin: 0em;
  padding: 1px 7px 2px;
  border-width: 1px;
  border-style: solid; */
  /* set a width of 100% to the parent's width (same for UL) */
  /* border-radius: 0 0.6em 0em 0; */
  background-color: rgb(186, 186, 186);
  border: solid thin;
  border-color: rgb(216, 216, 216) rgb(209, 209, 209) rgb(186, 186, 186);
  padding: 0.3rem;
  text-align: center;
}
li:first-of-type {
  border-radius: 0.6em 0.6em 0em 0;
}
li:last-of-type {
  border-radius: 0em 0em 0.6em 0.6em;
}
</style>
