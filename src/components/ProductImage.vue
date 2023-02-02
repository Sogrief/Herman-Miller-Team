<script>
export default {
  props: {
    images: {
      type: Array,
      default: () => [],
    },
  },
}
</script>

<template>
    <img :src=images[0].src>
</template>