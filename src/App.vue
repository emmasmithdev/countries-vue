<template>
  <div id="app">
    <h1>Countries</h1>
    <div class="main-container">
      <search-bar :country="searchCountry"></search-bar>
      <countries-list :countries="countries"></countries-list>
      <country-detail :country="selectedCountry"></country-detail>
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

    eventBus.$on('search-country', (country) => {
      this.selectedCountry = country
    })

    eventBus.$on('country-selected', (country) => {
      // let foundCountry = this.countries.find((countryObject){
      //   return countryObject.name === country
      // })
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
