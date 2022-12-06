<script>
export default {
  props: {
    nomProduit:String,
    prix:String,
    srcImage: String,
  },
};
</script>
<template>
  <div class="card">
    <div class="card__image">
      <img :src="srcImage"/>
    </div>
    <p class="card__title">{{ nomProduit }}</p>
    <p class="card__prix">{{ prix }}</p>
  </div>
</template>

<style lang="scss" scoped>

</style>