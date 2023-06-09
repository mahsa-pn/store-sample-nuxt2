<template>
  <div>
    <div class="container my-5">
      <div class="top">
        <h1 class="font-bold mb-4">Cart</h1>
      </div>
      <hr />
      <div class="row" v-if="cart.length > 0">
        <div class="col-md-3 p-2" v-for="(item, index) in cart" :key="index">
          <div class="card h-100 cart-item">
            <div class="btn remove" v-on:click="remove(index)">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="16"
                height="16"
                fill="currentColor"
                class="bi bi-trash"
                viewBox="0 0 16 16"
              >
                <path
                  d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5Zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5Zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6Z"
                />
                <path
                  d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1ZM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118ZM2.5 3h11V2h-11v1Z"
                />
              </svg>
            </div>
            <strong class="text-center">{{ item.product.attributes.name }}</strong>
            <span class="price">USD {{ item.product.attributes.price }}</span>
            <div class="counter">
              <div class="btn btn-secondary" v-on:click="reduce(index)">-</div>
              <div class="count">{{ item.count }}</div>
              <div class="btn btn-primary" v-on:click="add(index)">+</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  {{ test }}
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
export default {
  data(){
return{
    cart :[]
}
  },
  methods:{
     add  (index) {
      this.cart[index].count++;

     
    },
     reduce  (index) {
      this.cart[index].count--;
      if (this.cart[index].count <= 0) {
        this.cart.splice(index, 1);
      }

     
    },

     remove  (index) {
      this.cart.splice(index, 1);
     
    }
  },
  mounted(){
    this.cart = JSON.parse(localStorage.getItem("shoppingCart" || []));

  },
  watch:{
    cart:{
        handler(newValue){
            localStorage.setItem("shoppingCart", JSON.stringify(newValue));
        },
        deep:true
    }
  }
};
</script>

<style scoped>
.cart-item {
  align-items: center;
  padding: 1rem;
  justify-content: center;
}
.counter {
  display: flex;
  align-items: center;
  margin-top: 1rem;
}
.counter .btn {
  border-radius: 50%;
  width: 25px;
  height: 25px;
  padding: 0;
  align-items: center;
  display: flex;
  justify-content: center;
  line-height: 0;
  padding-bottom: 4px;
}
.counter .count {
  margin: 0 5px;
}
.card .remove {
  position: absolute;
  top: 10px;
  left: 10px;
  background: rgb(183, 26, 26);
  color: #fff;
  padding: 5px;
  border-radius: 5px;
  line-height: 0;
}
</style>
