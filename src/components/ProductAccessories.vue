<script>
import { client } from "@/outils/axios";
export default {
  props: {
    upsell_ids: {
      type: Array,
      default: () => [],
    },
  },
  async mounted() {
    const response = await client.get(
      import.meta.env.VITE_WP_API_URL +
        "/wc/v3/products?id=" +
        this.upsell_ids[0]
    );
    this.accessorie = response.data[0];
  },
};
</script>

<template>
  <div class="accessories">
    <p>{{ accessorie.name }}</p>
    <img :src="accessorie.images[0].src" />
    <p>{{ accessorie.price }}</p>
  </div>
</template>

<style lang="scss"></style>
