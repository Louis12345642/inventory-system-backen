
<script setup>
import ProductCartItem from "@/Pages/admin/products/productCartItem.vue";
import {computed} from "vue";
import { useForm } from '@inertiajs/vue3'
const props =defineProps({
    show:Boolean,
    products:Array

})

/*
* cartProducts: gets only the products that are added to cart
* prices :get the prices of the products added to the cart
* totalPrice() : a func that calculates the total price of the cartProducts
 */

const cartProducts = props.products.filter((product)=>product.added_cart === 1)
const prices = cartProducts.map((product)=>product.price)

const soldProducts = props.products.filter((product)=>product.sold === 1);

const totalPrice = computed(()=>{
    let price =0;
    for(let i =0; i<prices.length; i++){
        price+=prices[i]
    }
    return price;

})

//send all the cart products to the server
const sellForm = useForm({
    totalPrice
});

function  sell()
    {
        //send a post request to the server with the sold products
        sellForm.post(route('products.sell'))
    
    }

</script>

<template>
  <transition
enter-from-class="scale-125 opacity-0"
enter-to-class="scale-100 opacity-100"
enter-active-class="transition duration-300"
leave-active-class="transition duration-200"
leave-from-class="scale-100 opacity-100"
leave-to-class="scale-125 opacity-0"
  >
      <div v-if="show" class="model-mask">
          <div class="model-card">
              <div class="flex justify-between pb-2 pl-5 border-b-2" >
                  <h1 class="font-extrabold">Cart</h1>

                  <button  class="p-2 text-xs text-white bg-black rounded-md " @click="$emit('close')">CANCEL</button>

              </div>
             <!-- product carts are loaded here-->
              <ProductCartItem v-for="product in cartProducts" key="product.id" :product="product"/>

              <div class="flex justify-between pt-4 mt-4 border-t-2">
                <div class="flex gap-x-1.5">
                    <button @click="sell()" class="p-1 p-2 ml-5 text-xs font-extrabold text-white bg-blue-700 rounded-md">Purcase</button>
                    <button class="p-1 ml-5 text-xs font-extrabold text-white bg-black rounded-md ">Print Invoice</button>
                </div>

                  <h1 class="text-xs font-extrabold">Total price: ${{totalPrice}}</h1>
              </div>

          </div>
      </div>

  </transition>
</template>

<style>
.model-mask{
    position: fixed;
    top: 0;
    left: 0;
    background: rgba(0,0,0,.6);
    width: 100%;
    height: 100vh;
    display: grid;
    place-items: center;

}

.model-card{
    background: #ffffff;
    padding: 2rem;
    width: 60%;
  border: 1px solid darkgray;
  border-radius: 10px;
  box-shadow:5px 5px 5px 2px rgba(0,0,0,.1);

}
.products{
  display: flex;
  justify-content:space-between;
  margin: 1rem;
}
.product{
  display: flex;
  gap: 10px;

}
.product img{
  width: 60px;
  padding: 5px;
}
.image-wrapper{
  background: lightgrey;
  height: 50px;
}
.increment-btn{
  height: 30px;
  margin-top: 4px;
}
</style>

