<script setup lang="ts">
  import { cart } from '@/App.vue';
  import { computed } from 'vue';
  import type ProductType from '@/types/products';
  import { isCartOpen } from '@/App.vue';

  const itemPriceFormatter = (price: number, quantity: number) => {
    return (price * quantity).toLocaleString('pt-BR', {style: 'currency', currency: 'BRL'});
  }

  const totalPriceFormatter = computed(() => {
    let totalPrice = 0;

    for (let i = 0; i < cart.length ; i++) {
      totalPrice += (cart[i].price * cart[i].quantity)
    }

    return totalPrice.toLocaleString('pt-BR', {style: 'currency', currency: 'BRL'});
  })

  const removeFromCart = (item: ProductType) => {
    let itemInCart = cart.find(element => element.id === item.id);
    if (itemInCart) {
      cart.splice(cart.indexOf(itemInCart), 1)
    } else {
      return;
    }
  }
</script>

<template>
    <h2 class="fade-in" style="text-align: center;">Seu carrinho</h2>
  <div class="fade-in" id="cart">
    <div class="cart-content" v-if="cart.length > 0">
      <div class="cart-item" v-for="item in cart" v-show="item.quantity">
        <p>{{ item.name }}</p>
        <div><input type="number" v-model="item.quantity"></div>
        <p>{{ itemPriceFormatter(item.price, item.quantity) }}</p>
        <p style="color: red; cursor: pointer; text-align: right;" @click="removeFromCart(item)">x</p>
      </div>
      <br>
      <h3 style="text-align: right;">Valor total: {{ totalPriceFormatter }}</h3>
    </div>  
    <div class="fade-in" v-else>
      <p>Carrinho vazio 😑</p>
    </div>
  </div>
</template>

<style>

#cart {
  margin: 10px auto;

  width: 80%;
  padding: 20px;

  background-color: #f1f1f1;

  border-radius: 15px;

  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}

.cart-content {
  display: flex;
  flex-direction: column;
  gap: 1ch;
}

.cart-item {
  border: solid 1px #cccccc;
  border-radius: 15px;
  padding: 10px 20px;

  display: grid;
  grid-template-columns: 40% 20% 30% 10%;
}

.cart-item div {
  display: flex;
  justify-content: center;
  align-items: center;
}

.cart-item input {
  max-width: 40px;
  max-height: 40px;
  text-align: center;
}

.cart-item button {
  max-width:80%;

}

@media only screen and (max-width: 800px) {
  p {
    font-size: 0.9em;
  }

  #cart {
  margin: 5px;

  width: auto;

  max-width: 100%;
  padding: 10px;

  background-color: #f1f1f1;

  border-radius: 15px;

  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
  }

  .cart-item {
    padding: 10px 15px;
  }
}
</style>