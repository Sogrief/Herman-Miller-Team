<template>

  <MyHeader />

  <div class="categories">
    <MyButton label="filtre"/>
    <MyButton label="filtre"/>
    <MyButton label="filtre"/>
  </div>


  <div class="products-list">
    <div v-for="(product, index) in products" class="products-item column -size-3">
      <Product v-bind="product" />
    </div>
  </div>
</template>

<script>
import { client } from "@/outils/axios";
import MyHeader from "@/components/MyHeader.vue";
import Product from "@/components/Product.vue";
import MyButton from "@/components/MyButton.vue";

export default {
  components: { 
    Product,
    MyHeader,
    MyButton },

  data() {
    return {
      products: [],
      categorie:"all"
    };
  },

  computed:{
    filteredProducts(){
      return this.products.filter(function(product){

      })
    }
  },

  async mounted() {
    // Request products
    const productsResponse = await client.get(
      import.meta.env.VITE_WP_API_URL + "/wc/v3/products"
    );
    this.products = productsResponse.data;
  },
};
</script>

<style lang="scss">
  .products-list{
    display:flex;
    flex-wrap:wrap;
    justify-content: center;
    column-gap:3vw;
    row-gap:40px;
  }

</style>
