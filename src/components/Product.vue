<template>
    <div class="product" v-on:mouseover="hover = true" v-on:mouseleave="hover = false">
      <RouterLink :class="'product__link'" :to="`/boutique/${slug}`">
        <div v-if="cover" class="product__link__media">
          <img :class="'product__link__media__image'" :src="cover.src" :alt="cover.alt">
          <RouterLink class="product__link__media__buy" :to="`/boutique/${slug}`">
            <MyButton v-if="hover" label="acheter"/>
          </RouterLink>
        </div>
      </RouterLink>

      <p class="product__name">{{ name }}</p>
      <p class="product__price">{{ price }}€</p>
    </div>
</template>
  
<script>
  import MyButton from "@/components/MyButton.vue";

  export default {
    components: {
    MyButton,
    MyButton
  },

  data() {
    return {
      hover:false
    };
  },

    props: {
      name: {
        type: String,
        default: null
      },
      slug: {
        type: String,
        default: null
      },
      description: {
        type: String,
        default: null
      },
      price: {
        type: String,
        default: null
      },
      images: {
        type: Array,
        default: []
      }
    },

    computed: {
      cover () {
        if (!this.images.length) return
        const [cover] = this.images
        return cover
      }
    }
  }
       
</script>

<style lang="scss">

@import "./../scss/foundations/variables";

.product {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-image: url(/assets/images/encarts.png);
  background-size: 100% 100%;

  &__link {
    &__media {
      width: 25vw;
      display: flex;
      justify-content: center;
      align-items: center;

      &__image {
        width: 80%;
        filter: drop-shadow(0px 0px 25px rgb(67, 67, 67));
      }

      &__buy{
        filter: drop-shadow(0px 0px 70px black) drop-shadow(0px 0px 70px black) drop-shadow(0px 0px 70px black);
        position: absolute;
      }
    }
  }

  &__name {
    font-size: 20px;
    font-weight: 700;
    line-height: 26px;
    @include title();
  }

  &__price {
    font-size: 16px;
    font-weight: 700;
    margin-top: 10px;
    margin-bottom: 30px;
    @include bodyText();
  }
}

@media screen and (max-width: map-get($breakpoints, "tablet-down")) {
  .product__link__media {
    width: 40vw;
  }
}

@media screen and (max-width: map-get($breakpoints, "tablet-up")) {
  .product__link__media {
    width: 80vw;
  }
}
</style>
