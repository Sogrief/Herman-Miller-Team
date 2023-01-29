<template>

  <MyHeader />

  <div class="categories">
    <MyButton v-for="filtre in filtres" type="filtre" :label="filtre.label" :class="{'actif': filtre.isChecked}" @click="filtreCategory(filtre)">{{filtre.label}}</MyButton>
  </div>

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
      label: '',
      filtres: [
        { label: 'Bureau', isChecked: false},
        { label: 'Chaise', isChecked: false},
        { label: 'Accessoire', isChecked: false}
      ]
    };
  },

  methods:{
    filtreCategory(filtre) {
      this.label = filtre.label;



    if(filtre.isChecked==true)//si on reclique sur le même filtre ça le désactive
      {
        this.filtres.forEach(filtre=>{//on désactive tous les filtres
          filtre.isChecked=false;
        })

        this.label="";// on remet par défaut tous les produits
      }

      //à priori on souhaite que lorsqu'on clique sur un filtre un seul soit activé 
      //donc on les désactive tous puis on active seulement celui qui nous intéresse
      else{
        this.filtres.forEach(filtre=>{
            filtre.isChecked=false;
          })

          filtre.isChecked = !filtre.isChecked
      }
    },
  },

  computed:{
    
    filteredProducts(){
      const objet=this;

      if (objet.label === '') {//si aucune catégorie n'est sélectionnée on affiche tous les produits
      return this.products
      }

      else{
          return this.products.filter(function(product){
          return product.categories.includes(objet.label);
        })
      }
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

  .categories{
    display: flex;
    column-gap: 20px;
    margin-left:10vw;
    margin-bottom:65px;
  }

</style>
