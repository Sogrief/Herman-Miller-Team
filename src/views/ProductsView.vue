<template>

  <MyHeader />

  <div class="categories">
    <MyButton label="Bureau" @click="setLabel('Bureau')"/>
    <MyButton label="Chaise" @click="setLabel('Chaise')"/>
    <MyButton label="Accessoire" @click="setLabel('Accessoire')"/>
  </div>

  {{ this.label }}

  <div class="products-list">
    <div v-for="(product, index) in filteredProducts" class="products-item column -size-3">
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
      label: ''
    };
  },

  methods:{
    setLabel(label) {
      this.label = label;
      console.log(this.label)
    }
  },

  computed:{
    
    filteredProducts(){
      const objet=this;//filteredProducts à sa propre portée, il faut donc redéfinir this dans une constante
      return this.products.filter(function(product){
        return product.categories.includes(objet.label);
      })
    }
  },

  async mounted() {
    // Request products
    const productsResponse = await client.get(
      import.meta.env.VITE_WP_API_URL + "/wc/v3/products"
    );
    this.products = productsResponse.data;

    //mappin des categories
    this.products.forEach(product => {
      product.categories=product.categories.map(categorie => categorie.name);
    });
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
