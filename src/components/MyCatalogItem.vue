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
    <MyText size="-body" label="blabla" />
  </div>
</template>

<style lang="scss" scoped>
  .card
  {
    display:flex;
    flex-direction: column;
    align-items: center;
    
    &__title
    {
      @include title();
    }

    &__prix
    {
      @include bodyText();
    }
  }
</style>