<template>
  <div class="product-gallery">
    <div v-if="active" class="product-gallery__media">
      <img
        class="product-gallery__active"
        :src="active.src"
        :alt="active.alt"
      />
    </div>
    <div class="product-gallery__list">
      <div
        v-for="(image, index) in images"
        :class="[
          'product-gallery__item',
          { '-is-active': active.id === image.id },
        ]"
        :key="index"
        @click="changeImage(image)"
      >
        <div class="product-gallery__media">
          <img
            class="product-gallery__image"
            :src="image.src"
            :alt="image.alt"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    images: {
      type: Array,
      default: () => [],
    },
  },

  data() {
    return {
      active: this.images[0],
    };
  },

  methods: {
    changeImage(image) {
      this.active = image;
    },
  },
};
</script>

<style lang="scss">
.product-gallery {
  &__list {
    display: flex;
    flex-flow: row wrap;
  }

  &__item {
    width: 10%;

    &.-is-active {
      opacity: 0.5;
    }
  }

  &__media {
    overflow: hidden;
  }

  &__image {
    object-fit: cover;
    width: 100%;
  }
  &__active {
    width: 45%;
  }
}
</style>
