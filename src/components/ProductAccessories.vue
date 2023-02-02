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
            accessories: {},
            index: 0,
        }
    },
    props: {
        upsell_ids: {
            type: Array,
            default: () => [],
        },
    },
   
async created() {
  let accessories = [];
  for (let i = 0; i < this.upsell_ids.length; i++) {
    const response = await client.get(import.meta.env.VITE_WP_API_URL + "/wc/v3/products/" + this.upsell_ids[i]);
    accessories.push({
      index: i,
      data: response.data
    });
  }
  this.accessories = accessories;
}
}
</script>

<template>
    <div class="accessories">
        <MyTitle type="h2" class="-title" label="Ajout d'accessoires" />
    <div v-for="accessory in accessories" :key="accessory.index" class="accessories_card">
            <ProductImage class="accessories_img" v-if="accessory.data.images" :images="accessory.data.images"/>
            <p class="accessories_name">{{ accessory.data.name }}</p>
            <p class="accessories_price">{{ accessory.data.price }}€</p>
            <input class="accessories_checkbox" type="checkbox">
            <label class="accessories_check" for="myCheckbox"></label>
    </div>
  </div>
</template>

<style lang="scss">
.accessories{
    background-image: url('../../assets/images/accessorie_bg.svg');
    background-repeat: no-repeat;
    width: 440px;
    height: 310px;
    padding: 40px 0 0 50px;
    &_card{
        display: flex;
        gap: 25px;
        margin-top: 30px;
        align-items: center;
    }
    &_img{
        width: 60px;
        height:auto;
        object-fit: cover;
    }
    &_price{
        margin-left: 70px;
    }
    &_checkbox{
        display: none;
    }
    &_check {
        width: 15px;
        height: 15px;
        border: 1px solid $bodyText;
        cursor: pointer;
        display: inline-block;
    }
}
</style>