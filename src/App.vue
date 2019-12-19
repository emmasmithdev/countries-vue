<template>
  <div id="app">
    <h1>Countries</h1>
    <div class="main-container">
      <search-bar :country="searchCountry"></search-bar>
      <countries-list :countries="countries"></countries-list>
      <country-detail v-if="selectedCountry" :country="selectedCountry"></country-detail>
    </div>
  </div>
</template>

<script>
  import SearchBar from './components/SearchBar.vue';
  import CountryList from './components/CountryList.vue';
  import {eventBus} from './main.js';
  import CountryDetail from './components/CountryDetail.vue';

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null,
      searchCountry: null
    };
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on('search-country', (searchCountry) => {
      this.countries.forEach((country) => {
        if(searchCountry.length > 0){
          if(country.name.toLowerCase().indexOf(searchCountry) !== -1){
          }
        }
      })
      this.selectedCountry = country;
    })

    eventBus.$on('country-selected', (country) => {
      this.selectedCountry = country
    })
  },
  components: {
    "countries-list": CountryList,
    "country-detail": CountryDetail,
    "search-bar": SearchBar
  }
}
</script>

<style>
h1 {
  display: block;
  margin-left: auto;
  margin-right: auto;
  text-align: center;
}
.main-container {
  display: block;
  margin-right: auto;
  margin-left: auto;
  text-align: center;
}
</style>
