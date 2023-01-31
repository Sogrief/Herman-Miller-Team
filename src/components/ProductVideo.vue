<script>
export default {
  props: {
    meta_data: {
      type: Array,
      default: () => [],
    },
  },

  data() {
    return {
      active: this.meta_data[0],
    };
  },
};
</script>

<template>
  <iframe
    :src="active.value"
    title="YouTube video player"
    frameborder="0"
    class="product_video"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen
  ></iframe>
</template>

<style lang="scss">
.product_video {
  width: 100%;
  height: 100vh;
}
</style>
