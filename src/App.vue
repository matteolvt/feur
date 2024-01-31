<template>
  <div id="app">
    <!-- <div>
      <label>Mots clés : </label><input type="text" v-model="keywords">
    </div> -->

    <product-list :products="filteredProducts" @product-click="onProductClick($event)" />

    <div v-if="displayPopup === true" class="product-popup">
      <button @click="onPopupClose" class="popup-close-button">X</button>
      <product-details :product="displayedProduct"></product-details>
    </div>
  </div>
</template>

<script>

import axios from "axios";
import ProductDetails from "./components/ProductDetails.vue";
import ProductList from "./pages/ProductList.vue"


export default {
  name: 'App',
  components: {
    ProductDetails,
    ProductList,
  },
  data() {
    return {
      products: [],
      keywords: '',
      displayPopup: false,
      displayedProduct: null
    }
  },
  computed: {
    filteredProducts() {
      return this.products.filter(product => {
        return product.title.toLowerCase().includes(this.keywords.toLowerCase())
      });
    }
  },
  methods: {
    callback(response) {
      this.products = response.data.products;
    },
    getProducts() {
      axios.get('https://dummyjson.com/products')
        .then((response) => {
          const apiProducts = response.data.products;
          const VueProducts = apiProducts.map((product) => {
            if (product.category === 'smartphones') {
              product.component = 'SmartphoneCard';
              product.cssClass = 'smartphone-card';
            } else {
              product.component = 'ProductCard';
              product.cssClass = "product-card";
            }
            return product;
          });

          this.products = VueProducts;
        });
    },
    // getProductComponent(product) {
    //   if (product.category === "smartphones") {
    //     return 'SmartphoneCard'
    //   }
    //   return 'ProductCard';
    // },
    getProductClass(product) {
      if (product.category === 'smartphones') {
        return 'smartphone-card';
      }
    },
    wait(timeout) {
      return new Promise((resolve) => {
        setTimeout(resolve, timeout);
      });
    },
    onProductClick(product) {
      this.displayedProduct = product;
      this.displayPopup = true;
    },
    onPopupClose() {
      this.displayPopup = false;
    }
  },
  mounted() {
    this.getProducts();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}

.product-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.product-card {
  width: 350px;
  height: 300px;
  margin-top: 50px;
}

.product-card img {
  width: auto;
  height: 250px;
}

.smartphone-card {
  max-height: 200px;
  margin-top: 50px;
}

.product-popup {
  position: fixed;
  width: 600px;
  height: 600px;
  z-index: 100;
  top: 50%;
  left: 50%;
  background-color: #ffffff;
  border: 1px solid #000000;
  border-radius: 10px;
  transform: translate(-50%, -50%);
  color: #000000;
}

.popup-close-button {
  float: right;
}

body {
  background-color: #22311d;
}
</style>