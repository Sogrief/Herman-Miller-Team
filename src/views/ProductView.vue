<template>
  <MyHeader />
  <div class="product-view">
    <div class="product_container">
      <div class="product_img">
        <ProductCustom
          v-if="product.variations"
          :variations="product.variations"
        />
        <ProductGallery v-if="product.images" :images="product.images" />
      </div>
      <div class="product_info">
        <div class="product_header">
          <MyTitle :label="product.name"  class="-enormous" type="h1" />
          <p class="product-view__price">{{ product.price }}€</p>
        </div>
        
        <ProductAccessories v-if="product.upsell_ids" :upsell_ids="product.upsell_ids" />

        <div class="product_buy">
          <RouterLink :to="`/cart`" target="_blank">
            <MyButton class="button" label="Acheter" @click="buy()" />
          </RouterLink>
        </div>

      </div>
    </div>

    {{ this.$store.products }}

    <ProductVideo v-if="product.meta_data" :meta_data="product.meta_data" />

    <div class="product-view__description" v-html="product.description" />

    <ProductNav v-if="product.acf" :acf="product.acf" :image="product.acf.product_ergonomy" />

    <ProductSetUp v-if="product.cross_sell_ids" :cross_sell_ids="product.cross_sell_ids"/>

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
import ProductCustom from "../components/ProductCustom.vue";
import MyButton from "@/components/MyButton.vue";
import ProductNav from "@/components/ProductNav.vue";
import ProductAccessories from '@/components/ProductAccessories.vue'
import MyTitle from "../components/MyTitle.vue";
import ProductSetUp from "@/components/ProductSetUp.vue";

export default {
  components: {
    ProductCustom,
    ProductNav,
    ProductSetUp,
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
    buy(){
      this.$store.commit('add', this.product,this.quantity)
    }
  },
};
</script>

<style lang="scss">
.product {
  &_container {
    display: flex;
  }
  &-view__price{
    font-size: 30px;
    margin: 0;
    margin-bottom: 30px;
  }
  &_header{
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    .title-enormous{
    margin: 0;
  }
  }
  &_info{
    display: flex;
    flex-direction: column;
    align-items: end;
    width: 45%;
  }
  &_img {
    width: 45%;
    background-image: url("../../assets/images/product_bg.svg");
    background-size:cover;
  }
}
</style>
