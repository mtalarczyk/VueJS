<template>
  <div>
    <ul>
      <!-- <li v-for="p in products" :key="p.id">{{ p.name }}</li> -->
      <product-list-item v-for="p in products" :item="p" :key="p.id"></product-list-item>
    </ul>
    <p v-if="!products.length">No products!</p>
  </div>
</template>

<script>
  import ProductListItem from './ProductListItem';

  export default {
    name: "ProductList",
    // The case is, we have to define props (inputs)
    components: {
      ProductListItem
    },
    props: {
      // Here we also added some basic props validation
      products: {
        type: Array
      }
    }
  };
</script>

<style scoped>
</style>