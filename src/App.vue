<template>
  <div id="app">
    <h1> Welcome to CobraOnline </h1>
    <Organisms @organismChanged="organismChanged"/>
    <h4> App Data Model </h4>
    {{ selected_organism }}
  </div>
</template>

<script>
import Organisms from './components/Organisms.vue'
export default {
  name: 'App',
  components: {
    Organisms
  },
  data () {
    return {
      selected_organism: ''
    }
  },
  methods: {
    organismChanged: function (organism_id) {
      this.selected_organism = organism_id
    }
  }
}
</script>

<style>
</style>
