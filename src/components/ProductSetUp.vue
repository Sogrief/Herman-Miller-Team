<script>
import { client } from "@/outils/axios";
import ProductImage from './ProductImage.vue';
import MyTitle from './MyTitle.vue';
export default{
    components: {
        ProductImage,
        MyTitle,
    },
    data() {
        return{
            setup: {},
            index: 0,
        }
    },
    props: {
        cross_sell_ids: {
            type: Array,
            default: () => [],
        },
    },
   
async created() {
  let product = [];
  for (let i = 0; i < this.cross_sell_ids.length; i++) {
    const response = await client.get(import.meta.env.VITE_WP_API_URL + "/wc/v3/products/" + this.cross_sell_ids[i]);
    product.push({
      index: i,
      data: response.data
    });
  }
  this.setup = product;
},
}
</script>

<template>
    <div class="setup">
        <MyTitle type="h2" class="-title" label="Complétez votre set-up" />
    <div v-for="product in setup" :key="setup.index" class="setup_card">
            <ProductImage class="setup_img" v-if="product.data.images" :images="product.data.images"/>
            <p class="setup_name">{{ product.data.name }}</p>
            <p class="setup_price">{{ product.data.price }}€</p>
    </div>
  </div>
</template>

<style lang="scss">
</style>