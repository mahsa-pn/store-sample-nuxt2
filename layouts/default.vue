<template>
    <div class="content">
    
        <header class=" bg-light">
      <div class="container">
        <nav class="navbar navbar-expand-lg navbar-light">
  <a class="navbar-brand" href="/">Store</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="/">Products <span class="sr-only">(current)</span></a>
      </li>
     
    </ul>
    <nuxt-link to="/cart" class="cart-icon">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="25"
            height="25"
            fill="currentColor"
            class="bi bi-minecart mr-1"
            viewBox="0 0 16 16"
          >
            <path
              d="M4 15a1 1 0 1 1 0-2 1 1 0 0 1 0 2zm0 1a2 2 0 1 0 0-4 2 2 0 0 0 0 4zm8-1a1 1 0 1 1 0-2 1 1 0 0 1 0 2zm0 1a2 2 0 1 0 0-4 2 2 0 0 0 0 4zM.115 3.18A.5.5 0 0 1 .5 3h15a.5.5 0 0 1 .491.592l-1.5 8A.5.5 0 0 1 14 12H2a.5.5 0 0 1-.491-.408l-1.5-8a.5.5 0 0 1 .106-.411zm.987.82 1.313 7h11.17l1.313-7H1.102z"
            />
          </svg>
          Cart
          <div class="badge">{{ cartCount }}</div>
        </nuxt-link>
  </div>
</nav>
      </div>
        </header>
      <Nuxt />
      <footer>
        <span>Powered by Mahsa Pournjaf</span>
      </footer>
    </div>
  </template>

  <script>
export default {
    layout:'default1',
  data() {
    return {
      shoppingCart: [],
    };
  },
  computed: {
    cartCount: function () {
      let count = 0;
      for (var i = 0; i < this.shoppingCart.length; i++) {
        count += this.shoppingCart[i].count;
      }
      return count;
    },
  },
  mounted() {
    this.shoppingCart = JSON.parse(localStorage.getItem("shoppingCart" || []));
  },
};
</script>

<style>
.content{
    min-height: 100vh;
    display: flex;
    flex-direction: column;
}
footer{
    margin-top: auto;
    text-align: center;
    background: #565656;
    color: #fff;
    padding: 5px;
    font-size: 12px;
}
 .cart-icon {
  color: #333 !important;
  display: flex;
  align-items: center;
  justify-content: center;
}
 .cart-icon .badge {
  width: 25px;
  height: 25px;
  background: rgb(23, 23, 23);
  color: #fff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 5px;
}
</style>