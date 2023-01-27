<template>
  <MyHeader />
  <div class="product-view">
    <div class="container">
      <div class="product_img">
        <ProductCustom
          v-if="product.variations"
          :variations="product.variations"
        />
        <ProductGallery v-if="product.images" :images="product.images" />
      </div>
      <div class="container-header">
        <h1>{{ product.name }}</h1>
        <p class="product-view__price">{{ product.price }}€</p>
      </div>

      <div class="product_buy">
        <MyButton class="button" label="Acheter" @click="addToCart" />
        <MyButton class="button-quantite" label="-" />
        <MyButton class="button-quantite" label="+" />
      </div>

      <ProductVideo v-if="product.meta_data" :meta_data="product.meta_data" />

      <div class="product-view__description" v-html="product.description" />

      <ProductNav v-if="product.meta_data" :meta_data="product.meta_data" />

      {{ product.upsell_ids }}
    </div>
  </div>
  <MyFooter />
</template>

<script>
import { client } from "@/outils/axios";
import MyHeader from "@/components/MyHeader.vue";
import MyFooter from "@/components/MyFooter.vue";
import ProductVideo from "@/components/ProductVideo.vue";
import ProductGallery from "@/components/ProductGallery.vue";
import ProductCustom from "../components/ProductCustom.vue";
import MyButton from "@/components/MyButton.vue";
import ProductNav from "@/components/ProductNav.vue";

export default {
  components: {
    ProductCustom,
    ProductNav,
    MyHeader,
    MyFooter,
    ProductGallery,
    ProductVideo,
    MyButton,
  },

  data() {
    return {
      product: {},
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
    addToCart() {
      this.$store.commit("add", this.product);
    },
  },
};
</script>

<style lang="scss"></style>
