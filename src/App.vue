<template>
  <div id="app">
    <ProductDisplay v-if="productAvailable" />
    <ProductDisplay2 v-else />
  </div>
</template>

<script>
import ProductDisplay from './components/ProductDisplay.vue'
import ProductDisplay2 from './components/ProductDisplay2.vue'


export default {
  name: 'App',
  components: {
    ProductDisplay,
    ProductDisplay2,


  },
  data() {
    return {
      productAvailable: true // Mulai dengan menampilkan produk
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
