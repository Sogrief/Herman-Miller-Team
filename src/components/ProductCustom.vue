<script>
export default {
  props: {
    variations: {
      type: Array,
      default: () => [],
    },
  },

  data() {
    return {
      active: this.variations[0],
    };
  },
};
</script>

<template>
  {{ active }}
</template>

<style lang="scss"></style>
