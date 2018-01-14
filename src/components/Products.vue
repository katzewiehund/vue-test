<template>
<div>
  <h4>
    {{headline}}
    <span v-if="selected_organism_id.length>0">
      in model {{selected_organism_id}}
    </span>
  </h4>
  <input
     type="text"
     class="input"
     v-model="product_input"
     @keyup="inputChanged"
     >
  <ul>
    <li
       v-for="product in filtered_product_list"
       :key="product.value"
       @click="selectProduct(product.value, product.name)"
       >
      {{ product.name }}
    </li>
  </ul>
</div>
</template>

<script>
export default {
  data () {
    return {
      product_input: '',
      product_list: [
        { name: 'Pyruvate', value: 'pyr_c' },
        { name: 'Succinate', value: 'suc_c' },
        { name: 'Alanine', value: 'ala_c' }
      ],
      filtered_product_list: [],
      selected_product_id: null,
      max_results: 3
    }
  },
  props: ['headline', 'selected_organism_id'],
  methods: {
    inputChanged: function () {
      let lower_input = this.product_input.toLowerCase()
      if (lower_input.length > 0) {
        // update with content
        let number_results = 0
        this.filtered_product_list = []
        this.product_list.forEach(function (product) {
          if (product.name.toLowerCase().includes(lower_input)) {
            if (number_results < this.max_results) {
              this.filtered_product_list.push(product)
              number_results += 1
            }
          }
        }, this)
      } else {
        // no content
        this.filtered_product_list = []
        this.selected_product_id = ''
        this.$emit('productChanged', '')
      }
    },
    selectProduct: function (product, name) {
      this.product_input = name
      this.filtered_product_list = []
      this.selected_product_id = product
      this.$emit('productChanged', product)
    }
  },
  watch: {
    selected_organism_id: function (new_oid, old_oid) {
      console.log(new_oid)
      console.log(old_oid)
      // if the product cannot be found in the new model
      this.product_input = ''
      this.filtered_product_list = []
      this.$emit('productChanged', '')
    }
  },
  computed: {
  }
}
</script>

<style>
</style>
