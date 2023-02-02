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
            accessorie: {},
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
        // const response = await client.get(import.meta.env.VITE_WP_API_URL + "/wc/v3/products?id=" + this.upsell_ids[Index]);
        // this.accessorie = response.data[0]
        const makeRequest = () => {
        if (index === this.upsell_ids.length) return;
        const currentElement = upsell_ids.length[index];
        const response = client.get(import.meta.env.VITE_WP_API_URL + "/wc/v3/products?id=" + this.currentElement);
        this.accessorie = response.data[0]
        .then(response => {
            const access = client.get(import.meta.env.VITE_WP_API_URL + "/wc/v3/products?id=" + this.currentElement.id);
            this.accessorie = access.data[0]
      index++;
      makeRequest();
    })
};
    }
}
</script>

<template>
    <div class="accessories">
        <MyTitle type="h2" class="-title" label="Ajout d'accessoires" />
        <div class="accessories_card">
            <ProductImage class="accessories_img" v-if="accessorie.images" :images="accessorie.images"/>
            <p class="accessories_name">{{ accessorie.name }}</p>
            <p class="accessories_price">{{ accessorie.price }}€</p>
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