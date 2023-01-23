<template>
  <div class="product-view">
    <div class="container">
      <div class="row">
        <div class="column -size-6">
          route : {{ $route.params }}
          <br />
          wordpress data : {{ product }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {client} from "@/utils/axios"
export default {
  data () {
    return {
      product: {}
    }
  },

  async mounted () {
    const response = await client.get(import.meta.env.VITE_WP_API_URL + '/wc/v3/products?slug=' + this.$route.params.product)
    this.product = response.data;
  }
}
</script>

<style lang="scss">

</style>
