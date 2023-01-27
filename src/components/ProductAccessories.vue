<script>
export default {
  props: {
    upsell_ids: {
      type: Array,
      default: () => [],
    },
  },

  data() {
    return {
      upsell
    };
  },
};
</script>

<template>
  {{ active }}
</template>

<style lang="scss"></style>
