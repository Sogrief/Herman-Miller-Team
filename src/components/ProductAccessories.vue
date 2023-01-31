<script>
import { client } from '@/outils/axios';
import ProductImage from './ProductImage.vue';
export default{
    components: {
        ProductImage,
    },
    data() {
        return{
            accessorie: {},
        }
    },
    props: {
        upsell_ids: {
            type: Array,
            default: () => [],
        },
    },
    async created() {
        const response = await client.get(import.meta.env.VITE_WP_API_URL + "/wc/v3/products?id=" + this.upsell_ids[0]);
        this.accessorie = response.data[0]
    }
}
</script>

<template>
    <div class="accessories">
        <p>{{ accessorie.name }}</p>
        <p>{{ accessorie.price }}€</p>
        <ProductImage v-if="accessorie.images" :images="accessorie.images"/>
        <input class="checkbox" type="checkbox">
        <label class="check" for="myCheckbox"></label>
    </div>

</template>

<style lang="scss">
input[type="checkbox"] {
    display: none;
  }
  .check {
    width: 15px;
    height: 15px;
    border: 1px solid $bodyText;
    cursor: pointer;
    display: inline-block;
  }

  .accessories{
    background-image: url('../../assets/images/accessorie_bg.svg');
    background-repeat: no-repeat;
    display: flex;
  }
</style>