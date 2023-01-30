<template>
  <MyHeader />
  <div class="product-view">
    <div class="product_container">
      <div class="product_img">
        <!-- <ProductCustom
          v-if="product.variations"
          :variations="product.variations"
        /> -->
        <ProductGallery v-if="product.images" :images="product.images" />
      </div>
      <div class="product_info">
        <div class="product_header">
          <MyTitle :label="product.name"  class="-enormous" type="h1" />
          <p class="product-view__price">{{ product.price }}€</p>
        </div>
        
        <div class="product_buy">
          <MyButton class="button" label="Acheter" />
          <!-- Lier le bouton acheter vers le panier -->
          <MyButton
            class="button-quantite"
            label="-"
            @click="removeFromCart(1)"
          />
          <span>{{ quantity }}</span>
          <MyButton class="button-quantite" label="+" @click="addToCart(1)" />
        </div>
      </div>
    </div>

    <ProductAccessories v-if="product.upsell_ids" :upsell_ids="product.upsell_ids" />

    <ProductVideo v-if="product.meta_data" :meta_data="product.meta_data" />

    <div class="product-view__description" v-html="product.description" />

    <ProductNav v-if="product.acf" :acf="product.acf" :image="product.acf.product_ergonomy" />
  </div>
  <MyFooter />
</template>

<script>
import { client } from "@/outils/axios";
import MyHeader from "@/components/MyHeader.vue";
import MyFooter from "@/components/MyFooter.vue";
import Product from "@/components/Product.vue"
import ProductVideo from "@/components/ProductVideo.vue";
import ProductGallery from "@/components/ProductGallery.vue";
// import ProductCustom from "../components/ProductCustom.vue";
import MyButton from "@/components/MyButton.vue";
import ProductNav from "@/components/ProductNav.vue";
import ProductAccessories from '@/components/ProductAccessories.vue'
import MyTitle from "../components/MyTitle.vue";


export default {
  components: {
    // ProductCustom,
    ProductNav,
    MyHeader,
    Product,
    ProductAccessories,
    MyFooter,
    ProductGallery,
    ProductVideo,
    MyButton,
    MyTitle
},

  data() {
    return {
      product: {},
      inCart: false,
      quantity: 1,
    };
  },

  async mounted() {
    const response = await client.get(
      import.meta.env.VITE_WP_API_URL +
        "/wc/v3/products?slug=" +
        this.$route.params.product
    );
    this.product = response.data[0];
  },

  methods: {
    addToCart(quantity) {
      this.quantity += quantity;
      this.$store.commit("add", this.product);
    },
    removeFromCart(quantity) {
      this.quantity -= quantity;
      if (this.quantity < 0) this.quantity = 0;
      if (this.quantity === 0) this.inCart = false;
      this.$store.commit("remove", this.product);
    },
  },
};
</script>

<style lang="scss">
.product {
  &_container {
    display: flex;
  }
  &_img {
    width: 45%;
    background-image: url("../../assets/images/product_bg.svg");
    background-size:cover;
  }
}
</style>
