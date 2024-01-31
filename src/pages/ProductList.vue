<template>
    <div class="product-list">
        <template v-for="product in products">
            <component :is="product.component" :product="product" :key="product.id" :class="product.cssClass"
                @product-click="$emit('product-click', $event)"></component>
        </template>
    </div>
</template>

<script>
import SmartphoneCard from "../components/SmartphoneCard.vue";
import ProductCard from "../components/ProductCard.vue";

export default {
    name: 'ProductList',
    props: {
        products: {
            type: Array,
            default: null,
        },
    },
    components: {
        SmartphoneCard,
        ProductCard,
    }

}
</script>