<template>
    <div class="smartphone-container">
        <img src="../assets/iphone-svgrepo-com.svg" @click="$emit('product-click', product)">
        <div class="product-title">{{ product.title }}</div>
    </div>
</template>

<script>
export default {
    name: 'SmartphoneCard',
    props: {
        product: {
            type: Object,
            default: null,
        }
    }
}
</script>

<style scoped>
.smartphone-container {
    position: relative;
}

img {
    max-height: 200px;
    cursor: pointer;
}

.product-title {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    z-index: 100;
}
</style>