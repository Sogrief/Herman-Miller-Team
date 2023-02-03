<template>
  <MyHeader />
  <div class="product-view">
    <div class="product_container">
      <div class="product_img">

        <div class="custom">
          <div class="custom_points">
            <div class="custom_points_img">
              <img src="../../assets/images/product_point.svg" @click="openModal">
              <div v-if="showModal" class="modal-background">
                <div class="modal-content">
                 <MyTitle type="h3" :label="displayedProduct.attributes[0].name" class="-default" />
                <div v-if="colorAttribute" class="product-view__attribute">
                  <div v-for="(option, index) in colorAttribute.options" class="product-view__option" @click="changeColor(option)">
                    <p>{{ option }}</p>
                  </div>
                </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <ProductGallery v-if="displayedProduct.images" :images="displayedProduct.images" />
      </div>

      


      <div class="product_info">
        <div class="product_header">
          <MyTitle :label="displayedProduct.name"  class="-enormous" type="h1" />
          <p class="product-view__price">{{ displayedProduct.price }}€</p>
        </div>
        
        <ProductAccessories v-if="product.upsell_ids" :upsell_ids="product.upsell_ids" />

        <div class="product_buy">
          <MyButton  label="Acheter" @click="addToCart" />
        </div>
        

      </div>
    </div>

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
import MyCheckbox from "@/components/MyCheckbox.vue"
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
    MyCheckbox,
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
      variations: [],
      quantity: 1,
      activeColor: null,
      showModal: false,
    };
  },

  async mounted() {
    const response = await client.get(
      import.meta.env.VITE_WP_API_URL +
        "/wc/v3/products?slug=" +
        this.$route.params.product
    );
    this.product = response.data[0];
    if (this.product.type === 'variable') {
        for await (const id of this.product.variations) {
          const response = await client.get(import.meta.env.VITE_WP_API_URL + '/wc/v3/products/' + id)
          this.variations.push(response.data)
        }
        console.log(this.variations);
      }
  },

  computed: {
    colorAttribute () {
      if (!this.product.attributes) return
      return this.product.attributes.find(attribute => attribute.name === 'Couleur')
    },
    displayedProduct () {
      if (!this.activeColor) return this.product
      const [variation] = this.variations.filter((variation) => {
        return variation.attributes.find(attribute => attribute.option === this.activeColor)
      })
      return variation || this.product
    }
  },


  methods: {
    addToCart() {
      this.$store.commit("add", {product: this.displayedProduct});
    },
    closeModal() {
      this.showModal = false;
    },
    changeColor (color) {
      this.activeColor = color;
      this.closeModal();
    },
    openModal() {
      this.showModal = true;
    },
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
  &_buy{
    margin-top: 30px;
    width: 70%;
    display: flex;
    justify-content: center;
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

.custom{
  position: relative;
  &_points {
    position: relative;
    &_img{
      position: absolute;
      top: 180px;
      left: 250px;
    }
}
}

.modal-background {
  position: absolute;
  bottom: 40px;
  left: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  padding: 20px;
  border: 1px $mainColor solid;
  .title-default{
    margin: 0;
    margin-bottom: 10px;
  }
}

.product-view__attribute{
  display: flex;
  gap: 20px;
  width: 3%;
  cursor: pointer;
}
</style>
