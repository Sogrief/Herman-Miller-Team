<template>
    <div class="product">
      <RouterLink :class="'product__link'" :to="`/products/${slug}`">
        <div v-if="cover" class="product__link__media">
          <img :class="'product__link__media__image'" :src="cover.src" :alt="cover.alt">
        </div>
      </RouterLink>
      <p class="product__name">{{ name }}</p>
      <p class="product__price">{{ price }}€</p>
    </div>
  </template>
  
  <script>
  export default {
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
      },
      categories: {
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
  
  .product {
    display:flex;
    flex-direction:column;
    align-items: center;
    background-image: url(/assets/images/encarts.png);
    background-size: 100% 100%;
  
    &__link {

      &__media {
       width: 25vw;
       display:flex;
       justify-content: center;

        &__image {
          width: 80%;
          filter: drop-shadow(0px 0px 25px rgb(67, 67, 67));
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
      margin-bottom:30px;
      @include bodyText();
    }
  }
  </style>