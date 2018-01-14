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
       @click="selectOrganism(organism.value)"
       >
      {{ organism.name }}
    </li>
  </ul>
</div>
</template>

<script>
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
  props: ['selected_product_id'],
  methods: {
    inputChanged: function () {
      let lower_input = this.organism_input.toLowerCase()
      console.log('Input changed')
      console.log(lower_input)
      console.log(this.organism_input)
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
    },
    selectOrganism: function (organism) {
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
