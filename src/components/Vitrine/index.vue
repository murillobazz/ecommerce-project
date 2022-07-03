
<template>
  <div id="vitrine">
    <VitrineItem v-for="product in productsList" :product="product" :id="product.id" :name="product.name"
      :image="product.image" :price="product.price" :quantity="product.quantity"/>

  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import VitrineItem from "@/components/Vitrine/VitrineItem/index.vue"
import type { PropType } from "vue";
import type ProductType from "@/types/products";

export default defineComponent({
  name: "Vitrine",
  components: {
    VitrineItem
  },
  props: {
    productsList: {
      required: true,
      type: Array as PropType<ProductType[]>
    },
  }
})

</script>
<style>
#vitrine {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  gap: 1em;

  padding: 10px 20px;
}

@media only screen and (max-width: 800px) {
  #vitrine {
    grid-template-columns: auto auto;
    gap: 0.5em;

    padding: 5px;
    margin-bottom: 20px;
  }
}
</style>