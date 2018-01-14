<template>
<div>
  <h4> Organism </h4>
  <input
     type="text"
     class="input"
     v-model="organism_input"
     @keyup="inputChanged"
     >
  <ul>
    <li
       v-for="organism in filtered_organism_list"
       :key="organism.value"
       @click="selectOrganism(organism.value, organism.name)"
       >
      {{ organism.name }}
    </li>
  </ul>
</div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      organism_input: '',
      organism_list: [
        { name: 'Saccharomyces cerevisiae', value: 'iSH654' },
        { name: 'Escherichia coli', value: 'iAD123' }
      ],
      filtered_organism_list: [],
      selected_organism_id: null,
      max_results: 3
    }
  },
  created () {
    console.log('created')
    this.getOrganismList()
  },
  props: ['selected_product_id'],
  methods: {
    getOrganismList: function () {
      axios.get('http://jsonplaceholder.typicode.com/todos')
        .then((response) => {
          this.organism_list = []
          response.data.forEach(function (d) {
            this.organism_list.push({ name: d.title, value: d.id })
          }, this)
        })
    },
    inputChanged: function () {
      let lower_input = this.organism_input.toLowerCase()
      if (lower_input.length > 0) {
        let number_results = 0
        this.filtered_organism_list = []
        this.organism_list.forEach(function (organism) {
          if (organism.name.toLowerCase().includes(lower_input)) {
            if (number_results < this.max_results) {
              this.filtered_organism_list.push(organism)
              number_results += 1
            }
          }
        }, this)
      } else {
        this.filtered_organism_list = []
        this.selected_organism_id = ''
        this.$emit('organismChanged', '')
      }
    },
    selectOrganism: function (organism, name) {
      this.organism_input = name
      this.filtered_organism_list = []
      this.selected_organism_id = organism
      this.$emit('organismChanged', organism)
    }
  },
  computed: {
  }
}
</script>

<style>
</style>
