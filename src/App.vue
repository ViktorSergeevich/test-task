<template>
<div id="app" class="grid container">
  <div class="sub_category_page">
    <div class="column_right column_right_products_container">
      <div class="product_area">
        <productSection />
      </div>
    </div>
  </div>
</div>

</template>

<script>

import productSection from "./components/products_section.vue"
export default {
  name: 'App',
  components: {
    productSection
  }
}
</script>

<style>

</style>
