<template>
  <div class="showcase">
    <productItem v-for="(product, index) in products" :key="index" :product="product" :price="prices[index]" :inputAut="inputAut"/>
  </div>
</template>

<script>
import productItem from '../components/product.vue'

export default {
  name: 'showCase',
  data() {
    return {
      products: ['colombiana.jpg', 'coca-cola.jpg', 'manzana200.png', 'manzana400.jpg', 'manzana500.jpeg', 'uva200.png', 'uva500.jpeg', 'coca-cola400.jpg', 'uva250.jpg'],
      prices: ['$ 3.000', '$ 3.500', '$ 2.000', '$ 4.000', '$ 5.000', '$ 2.000', '$ 5.000', '$ 5.000', '$ 2.500']
    };
  },
  components: {
    productItem
  },
  props:{
    inputAut: String
  }
}
</script>

<style scoped>
.showcase {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 15px; 
}
</style>
