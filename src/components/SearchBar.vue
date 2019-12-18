<template lang="html">
  <div>
    <label for="search">Search for a country:</label><br>
    <input type="text" name="search" value="searchCountry" v-model="searchCountry"
    @input="handleSearch">
  </div>
</template>

<script>
  import {eventBus} from '../main.js'

export default {
  name: 'search-bar',
  data(){
    return{
      searchCountry: null
    }
  },
  props: ['countries'],
  methods: {
    handleSearch(event){
      // for (country in this.countries){
      //   if (country.name === this.searchCountry){
      //     return country
      //   }
      // }
      eventBus.$emit('search-country', this.searchCountry)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
