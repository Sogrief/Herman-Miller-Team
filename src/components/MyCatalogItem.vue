<script>
import MyText from "../components/MyText.vue";

export default {
    props: {
        nomProduit: String,
        prix: String,
        srcImage: String,
    },
    components: { 
      MyText, 
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
    <MyText size="-body" />
  </div>
</template>

<style lang="scss" scoped>
  .card
  {
    display: flex;
    flex-direction: column;
    align-items: center;
    width:pxToRem(332);
    height:pxToRem(544);

    &__image
    {
      img
      {
        height:pxToRem(300);
      }
    }
    
    &__title
    {
      @include title();
      margin-top:pxToRem(50);
    }

    &__prix
    {
      @include bodyText();
    }
  }
</style>