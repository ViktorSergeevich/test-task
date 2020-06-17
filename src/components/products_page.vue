<template>
  
  <div class="products_page">
      <product 
        v-for="product in PRODUCTS"
        :key="product.productId"
        :product_data="product"
      />
  </div>
  
</template>

<script>

import product from "./product"
import {mapActions, mapGetters} from 'vuex'


export default {
    name: "products-page",
    components: {
        product
    }, 
    computed: {
        ...mapGetters([
            'PRODUCTS'
        ])
    },
    methods: {
        ...mapActions([
            'GET_PRODUCTS_FROM_API'
        ]),
    },
    prop: {},
    mounted() {
        this.GET_PRODUCTS_FROM_API()
    }
}
</script>

<style>

</style>