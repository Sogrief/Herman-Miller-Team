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
        <MyTitle type="h2" class="-title setup_title" label="Complétez votre set-up" />
        <div class="setup_container">
        <div v-for="product in setup" :key="setup.index" class="setup_card">
          <RouterLink class="product__link__media__buy" :to="'/boutique/' + product.data.slug" >
            <ProductImage class="setup_img" v-if="product.data.images" :images="product.data.images"/>
            <div class="setup_info">
              <MyTitle type="h3" class="-default" :label="product.data.name" />
              <p class="setup_price">{{ product.data.price }}€</p>
            </div>
          </RouterLink>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.setup{
  &_title{
    margin-top: 90px;
    padding-left: 70px;
    margin-left: 25px;
    background-image: url('../../assets/images/title_bg.svg');
    background-repeat: no-repeat;
  }
  &_img{
    width: 70%;
    height: 70%;
    object-fit: cover;
    filter: drop-shadow(0px 0px 25px rgb(67, 67, 67));
  }
  &_info{
    display: flex;
    gap: 50px;
  }
  &_container{
    display: flex;
    justify-content: center;
  }
}
</style>
