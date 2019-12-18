<template lang="html">
  <div v-if="country">
    <h3>{{country.name}}</h3>
    <p>Region: {{country.region}}</p>
    <p>Population: {{country.population}}</p>
    <h4>Languages:</h4>
    <p v-for="(language, index) in country.languages" :language="language"
    :key="index" :value="language.name">{{language.name}}</p>
    <img class="flag" :src="country.flag" />
  </div>
</template>

<script>
export default {
  name: "country-detail",
  props: ["country"]
}
</script>

<style lang="css" scoped>
  .flag {
    width: 300px;
    height: 200px;
  }
</style>
