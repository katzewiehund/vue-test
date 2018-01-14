<template>
  <div id="app">
    <h1> Welcome to CobraOnline </h1>
    <h4> Organism </h4>
    <input v-model="organism_input"> </input>
    <button v-on:click="updateOrganism">Press me</button>
    <div v-if="show_result">
      Result: {{ selected_organism }}
      <ol>
        <li v-for="organism in organisms"> {{ organism.name }} </li>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
    name: 'App',
    data() {
	return {
	    message: 'Hello World',
	    show_result: true,
	    organism_input: '',
	    selected_organism: '',
	    organisms: [
	        { name: 'Saccharomyces cerevisiae', value: 'iSH654' },
	        { name: 'Escherichia coli', value: 'iAD123' }
	    ]
	}
    },
    methods: {
        updateOrganism: function(){
	    this.selected_organism = this.organism_input;
	    this.show_result = !this.show_result;
	}
    }
}
</script>

<style>
</style>
