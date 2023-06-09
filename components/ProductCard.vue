<template>
    <div class="card">
        <!-- <img :src="product.image" class="thumb mx-auto" alt=""> -->
        <p class="text-bold text-center mt-0 mb-2">{{ product.attributes.name }}</p>
        <span>USD {{ product.attributes.price }}</span>
        <div class="btn" v-on:click="addToCart(product)">Add to cart</div>

    </div>
</template>

<script>
import { onMounted, ref } from 'vue';
import {state , actions} from "../store/index"

export default{
    props:["product"],
    setup(props,{emit}){

        const action = ref(actions)


        onMounted(()=>{
        })

        const addToCart =(product)=>{
            // actions.addToCart(product)
            emit('addToCart',product)
        }
      return {addToCart,action}
    }
}

</script>

<style scoped >
.card{
    border: 1px solid gainsboro;
    padding: 1rem;
    border-radius: 5px;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.thumb{
    height: 120px;
    object-fit: contain;
    width: 100%;
    max-width: 70%;
}
.btn{
    background-color: cornflowerblue;
    color: #fff;
    padding: 5px;
    width: 100%;
    display: flex;
    justify-content: center;
    margin-top: 5px !important;
    border-radius: 5px;
    margin-top: auto;
}
</style>