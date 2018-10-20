<template>
  <form @submit.prevent="onSubmit()">
    <input
      v-validate="'required|min:3'"
      v-model="newProduct.name"  
      name="product"      
    >
    <button>Add</button>
    <div v-show="errors.has('product')">
      {{ errors.first('product') }}
    </div>
  </form>
</template>

<script>
  import uuid from 'uuid/v4';

  export default {
    name: "AddProduct",
    //6/ newProduct goes to AddProduct component
    data() {
      return {
        newProduct: {
          name: ''
        }
      }
    },
    //3/ As well as onSubmit
    methods: {
      onSubmit() {
        this.$validator.validateAll().then(result => {
          if (!result) {
            return;
          }
          //4/ But instead of adding element we're just emitting add-product event with product as a payload
          this.$emit('add-product', {
            id: uuid(),
            ...this.newProduct
          });
          this.newProduct.name = '';
          this.$validator.reset();
        });
      },
      removeLast() {
        this.products.pop();
      }
    }
  }
</script>

<style scoped></style>