<template>
  <div id="app">
    <h1> Welcome to CobraOnline </h1>
    <Organisms @organismChanged="organismChanged"/>
    <Products headline="Product"
              @productChanged="productChanged"
              :selected_organism_id="selected_organism"/>
    <Products headline="Substrate"
              @productChanged="substrateChanged"
              :selected_organism_id="selected_organism"/>
    <h4> App Data Model </h4>
    <div> Selected organism: {{ selected_organism }} </div>
    <div> Selected product: {{ selected_product }} </div>
    <div> Selected substrate: {{ selected_substrate }} </div>
  </div>
</template>

<script>
import Organisms from './components/Organisms.vue'
import Products from './components/Products.vue'
export default {
  name: 'App',
  components: {
    Organisms,
    Products
  },
  data () {
    return {
      selected_organism: '',
      selected_product: '',
      selected_substrate: ''
    }
  },
  methods: {
    organismChanged: function (organism_id) {
      this.selected_organism = organism_id
    },
    productChanged: function (product_id) {
      this.selected_product = product_id
    },
    substrateChanged: function (product_id) {
      this.selected_substrate = product_id
    }
  }
}
</script>

<style>
</style>
