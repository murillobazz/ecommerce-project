<script setup lang="ts">
  import Vitrine from './components/Vitrine/index.vue';
  import ShoppingCart from './components/ShoppingCart/index.vue';
  import { ref, reactive } from 'vue';
  import type ProductType from '@/types/products';
  import Swal from 'sweetalert2';
  
  const productsList: ProductType[] = [];
  const fetchProducts = async () => {
    const apiResponse = await fetch('https://run.mocky.io/v3/fe19fbfa-83a4-48c8-b66d-b8b7ae607ef7')
    const products = await apiResponse.json();
    productsList.push(...products);
    console.log(productsList)
  }
  fetchProducts();


</script>

<template>
  <header>
    <h1>Cabum>></h1>
    <img class="fade-in" src="./assets/shopping-cart.svg" @click="isCartOpen = !isCartOpen" v-if="!isCartOpen"/>
    <img class="fade-in" src="./assets/x.svg" @click="isCartOpen = !isCartOpen" style="padding: 10px;" v-else/>
  </header>
  <main>
    <div v-if="!isCartOpen" class="fade-in">
      <h2 style="text-align: center;">Produtos</h2>
      <Vitrine :productsList="productsList"/>
    </div>
    <ShoppingCart v-else/>

  </main>
</template>
<script lang="ts">
  export const cart: ProductType[] = reactive([]);

  export const isCartOpen = ref(true);

  export const addToCart = (item: ProductType) => {
    let itemInCart = cart.find(element => element.id === item.id);
    if (itemInCart) {
      itemInCart.quantity++
      console.log("Item já estava no carrinho ;)");
      console.log(cart);
      addItemAlert();
    } else {
      cart.push({...item});
      console.log("Novo item!");
      console.log(cart);
      addItemAlert();
    }

  }

  const addItemAlert = () => {
    Swal.fire({
      position: 'top',
      title: 'Adicionado ao carrinho!',
      icon: 'success',
      showConfirmButton: false,
      allowOutsideClick: false,
      timerProgressBar: true,
      timer: 1500,
      width: 300,
      
    })
  }

</script>

<style>
@import './assets/global.css';

header {
  height: 40px;
  padding: 5px 10px;
  display: flex;
  justify-content: space-between;
  border-bottom: solid 0.5px rgb(204, 204, 204);
}

header h1 {
  color: #ff7300;
  margin: 0;
}

header img {
  padding: 5px 10px;
}

header img:hover {
  cursor: pointer;
}


</style>
