<template>
  <div class="product-view">
    <div class="container">
      <div class="product_img">
        <ProductGallery v-if="product.images" :images="product.images" />
      </div>
      <div class="container-header">
        <h1>{{ product.name }}</h1>
        <p class="product-view__price">{{ product.price }}€</p>

        <ProductVideo v-if="product.meta_data" :meta_data="product.meta_data" />
      </div>

      <div class="product-view__description" v-html="product.description" />

      <div class="product_buy">
        <MyButton class="button" label="Acheter" />
        <MyButton class="button-quantite" label="-" />
        <MyButton class="button-quantite" label="+" />
        <p>{{ product.upsell_ids }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { client } from "@/outils/axios";
import ProductVideo from "@/components/ProductVideo.vue"
import ProductGallery from "@/components/ProductGallery.vue";
import MyButton from "@/components/MyButton.vue";

export default {
  components: {
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

};

</script>

<style lang="scss">
// .product {
//   &-video > div {
//     & > video {
//       height: 100%;
//     }
//   }
// }
// .wp-video{
//   width: 100px;
// }
</style>
