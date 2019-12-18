<template lang="html">
  <div>
      <label for="country_select">Select a Country:</label><br>
          <select id="country_select" @change="handleChange" v-model="selectedCountry">
            <option disabled value="">Select a country</option>
            <option v-for="(country, index) in countries" :country="country" :key="index" :value="country">{{country.name}}</option>
          </select>
  </div>
</template>

<script>
  import {eventBus} from '../main.js';
  import ListItem from './ListItem.vue';

export default {
  name: 'countries-list',
  data(){
    return {
        selectedCountry: null
    }
  },
  props: ['countries'],

  components: {
    "list-item": ListItem
  },
  methods: {
    handleChange(event){
      eventBus.$emit('country-selected', this.selectedCountry)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
