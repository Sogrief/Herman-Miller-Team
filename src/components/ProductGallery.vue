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
    watch: {
    images (value) {
      this.active = value[0]
    }
  },
    changeImage(image) {
      this.active = image;
    },
  },
};
</script>

<style lang="scss">
.product-gallery {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 40px;
  &__list {
    display: flex;
    justify-content: center;
    flex-flow: row wrap;
    width: fit-content;
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
    width: 100%;
  }
}
</style>
