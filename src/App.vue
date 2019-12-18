<template>
  <div id="app">
    <h1>Countries</h1>
    <div class="main-container">
      <countries-list :countries="countries"></countries-list>
      <country-detail :country="selectedCountry"></country-detail>
    </div>
  </div>
</template>

<script>
  import CountryList from './components/CountryList.vue';
  import {eventBus} from './main.js';
  import CountryDetail from './components/CountryDetail.vue';

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null
    };
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on('country-selected', (country) => {
      this.selectedCountry = country
    })
  },
  components: {
    "countries-list": CountryList,
    "country-detail": CountryDetail
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
  display: flex;
  justify-content: space-around;
  margin-right: 40px;
}
</style>
