<template>
    <div>
        <section v-if="error">
            {{error.message}}
        </section>
        <section v-else>
        <div v-if="loading">
            <h2>Loading products...</h2>
        </div>
        <product-list v-else :products="products" :page-size="5"></product-list>
        </section>
    </div>
</template>

<script>
import ProductList from '@/components/ProductList.vue';

export default {
  name: 'app',
  components: {
    ProductList
  },
  data() {
    return {
      error: null
    }
  },
  computed: {
      products() {
        return this.$store.state.products;
      },
      loading() {
        return this.$store.state.isLoading;
      }
  },
  methods: {
    fetchProducts() {
      this
        .$store
        .dispatch('fetchProducts')
        .catch(error => {
          this.error = error;
        });
    }
  },
  created () {
    this.fetchProducts();
  }
}
</script>

<style lang="scss" scoped>

</style>