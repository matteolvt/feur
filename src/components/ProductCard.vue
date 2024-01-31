<template>
  <div class="card-layout">
    <div><img :src="product.thumbnail" @click="onThumbnailClick" /></div>
    <div class="product-details">
      <div>{{ product.title }}</div>
      <div class="product-price">{{ product.price }} €</div>
    </div>
  </div>
</template>
<script>
export default {
  name: "ProductCard",
  emit: [
    'product-click'
  ],
  props: {
    product: {
      type: Object,
      default: null,
    },
  },
  emits: ['product-click'],
  methods: {
    onThumbnailClick() {
      this.$emit('product-click', this.product);
    }
  }
};
</script>
<style scoped>
.card-layout {
  display: flex;
  flex-direction: column;
}

img {
  max-width: 100%;
  max-height: 100%;
  cursor: pointer;
}

.product-details {
  display: flex;
  justify-content: space-between;
}

.product-price {
  font-weight: bold;
  text-align: right;
}
</style>