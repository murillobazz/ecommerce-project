<script lang="ts">
import { addToCart } from '@/App.vue'
</script>

<template>
  <div id="vitrine-item">
    <img :src="product.image" alt="">
    <h2>{{ product.name }}</h2>
    <h3>{{ product.price.toLocaleString('pt-BR', {style: 'currency', currency: 'BRL'}) }}</h3>
    <button @click="addToCart(product)">Adicionar ao carrinho</button>
  </div>

</template>

<script setup lang="ts">

type ProductType = {
  id: number
  name: string
  price: number
  image?: string
  quantity: any
}

const product = defineProps<ProductType>();

</script>

<style>
#vitrine-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  place-self: center;

  min-width: 240px;
  max-width: 360px;
  padding: 10px 20px;

  background-color: #f1f1f1;

  border-radius: 15px;

  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}

#vitrine-item h2,
h3 {
  margin: 0 0 10px 0;
}

#vitrine-item img {
  max-width: 100px;
  max-height: 100px;
}

@media only screen and (max-width: 800px) {
  #vitrine-item {
    min-width: auto;
    max-width: 160px;
    padding: 15px 5px;
  }

  #vitrine-item img {
    max-width: 75px;
    max-height: 75px;
  }

  #vitrine-item h2 {
    font-size: 1.2rem;
  }

  #vitrine-item h3 {
    font-size: 1rem;
  }

  #vitrine-item button {
    padding: 5px 10px;
  }
}
</style>