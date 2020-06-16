<template>
  <div id="app">
    <section v-if="error">
      {{error.message}}
    </section>
    <section v-else>
        <div v-if="loading">
          <h2>Loading products...</h2>
        </div>
        <product-list v-else :products="products"></product-list>
    </section>
  </div>
</template>

<script>
import ProductList from '@/components/ProductList.vue';
import ProductService from '@/services/ProductService.js';

export default {
  name: 'App',
  components: {
    ProductList
  },
  data() {
    return {
      products: [],
      error: null,
      loading: false
    }
  },
  created () {
    this.loading = true;
      ProductService
        .getProducts()
        .then(response => {
          this.products = response.data
        })
        .catch(error => {
          this.error = error;
        })
        .finally(
          () => this.loading = false
        );
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
