<template>

  <MyHeader />

  <div class="categories">
    <MyButton label="filtre"/>
    <MyButton label="filtre"/>
    <MyButton label="filtre"/>
  </div>

  {{ this.categorie }}
<div v-for="product in products">
  <div v-for="category in product.categories">
    {{category.name}}
    
  </div>
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
      categorie:[]
    };
  },

  methods: {
    getCategories() {
      for (let i = 0; i < this.products.length; i++) {
        let product = this.products[i];

        for (let j = 0; j < product.categories.length; j++) {
          let category = product.categories[j];
          this.categorie.push(category.name);
        }
      }
    }
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

    this.getCategories();
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
