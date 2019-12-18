<template lang="html">
  <div>

      <!-- <list-item v-for="(country, index) in countries" :country="country" :key="index"></list-item> -->
      <label for="country_select">Select a Country:</label>
          <select id="country_select" @change="handleChange">
            <option disabled value="">Select a country</option>
            <option v-for="(country, index) in countries" :country="country" :key="index">{{country.name}}</option>
          </select>
  </div>
</template>

<script>
  import ListItem from './ListItem.vue';

export default {
  name: 'countries-list',
  props: ['countries'],
  components: {
    "list-item": ListItem
  },
  methods: {
    handleChange(){
      eventBus.$emit('country-selected', this.country)
    }
  }

}
</script>

<style lang="css" scoped>
</style>
