<template>
  <div id="app">
    <h2>My awesome list</h2>
    <!-- 3. Then we can use component by kebab-cased name and providing :input -->
    <!-- <product-list :products="products"></product-list> -->
    <product-list :products="sharedState.products"></product-list>
    
    <!-- With @ we can listen to add-product event and assign onAddProduct-->
    <add-product @add-product="onAddProduct"></add-product>
  </div>
</template>

<script>
// 1. To use our new, shiny component we need to import it first
import ProductList from './components/ProductList';
import AddProduct from './components/AddProduct';
// import axios from 'axios';
import store from '../store';

export default {
  name: 'app',
  //3/ 2. And add it to as a key called 'components'
  components: {
    ProductList,
    AddProduct
  },
  created() {
    store.fetchProducts();
  },
  data() {
    return {
      sharedState: store.state

      //products: []
      
      // LUB:

      // products: [{
      //   id: 0,
      //   name: 'Coffee'
      // }, {
      //   id: 1,
      //   name: 'Pizza'
      // }]
    }
  },
  methods: {
    //3/ All we have to do in a method is to add product to the list
    onAddProduct(product) {
      // this.products.push(product);
      store.addProduct(product);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>