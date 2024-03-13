<template>
  <div class="product">
    <div class="product-img">
      <img :src="require(`@/assets/${product}`)" :alt="product">
    </div>
    <div class="price">
      <p>{{ price }}</p>
    </div>
    <div class="allow">
      <div class="red"></div>
      <div :class="{ 'green': !isPProduct, 'green-true': isPProduct && (product.includes('uva') || product.includes('manzana')) }"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'productItem',
  props: {
    product: String,
    price: String,
    inputAut: String
  }
}
</script>

<style scoped>
.product {
  width: 80px;
  height: 120px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 15px;
  border: 2px solid #ccc;
  border-radius: 8px;
  margin: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.product-img img {
  width: 100%;
  border-radius: 6px;
}

.price {
  margin-top: 8px;
  font-size: 1em;
  font-weight: bold;
  color: #333;
}

.allow {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.red, .green, .green-true {
  width: 47%;
  height: 11px;
  border-radius: 4px;
}

.red {
  background-color: #8B0000;
}

.green {
  background-color: #006400;
}
.green-true {
  background-color: #3ad13a;
}
</style>
