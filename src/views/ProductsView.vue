<template>
  <div class="products-view">
    <div class="container">
      <div class="products-wrapper">
        <div class="column -size-9">
          <div class="products-list row">
            <div
              v-for="(product, index) in products"
              class="products-item column -size-3"
            >
              <Product v-bind="product" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { client } from "@/outils/axios";
import Product from "@/components/Product.vue";

export default {
  components: { Product },

  data() {
    return {
      products: [],
      price: "2000",
    };
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

<style lang="scss"></style>
