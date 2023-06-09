<template>
  <div>
    <div class="container my-5">
      <div class="top">
        <h1 class="font-bold mb-4">Products</h1>
        
      </div>
      <hr />
      <div class="row">
        <div
          class="col-md-3 p-2"
          v-for="(item, index) in products"
          :key="index"
        >
          <ProductCard :product="item" @addToCart="addToCart" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
    layout:'default1',
  data() {
    return {
      products: [],
      shoppingCart:[]
    };
  },
  methods: {
    addToCart(product) {
      let exist = null;
      for (var i = 0; i < this.shoppingCart.length; i++) {
        if (product.id == this.shoppingCart[i].product.id) {
          exist = i;
        }
      }

      if (exist != null) {
        this.shoppingCart[exist].count++;
      } else {
        this.shoppingCart.push({
          product: product,
          count: 1,
        });
      }

      localStorage.setItem("shoppingCart", JSON.stringify(this.shoppingCart));
    },
  },
  mounted(){
    this.shoppingCart = JSON.parse(localStorage.getItem("shoppingCart" || []));

  },
  async fetch() {
    const response = await fetch(
      "https://demo.spreecommerce.org/api/v2/storefront/products"
    );
    this.products = (await response.json()).data;
  },
};
</script>

<style scoped>
.top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

</style>
