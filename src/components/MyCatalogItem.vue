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
    <img :src="srcImage"/>
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
    justify-content: center;
    width:pxToRem(332);
    height:pxToRem(544);
    border:1px solid $mainColor;

    
    img
    {
      //box-shadow: 0px 0px 179px -81px rgba(155, 155, 155, 0.71);
      height:pxToRem(300);
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