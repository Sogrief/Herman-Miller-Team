<script>
import MyTitle from "./MyTitle.vue";
export default {
  components: {
    MyTitle,
  },
  props: {
    acf: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<template>
  <div class="bg-perspective">
    <div class=" infoCard" v-if="acf.infos">
      <div
        class="infoCard__image"
        v-for="item in acf.infos"
        :key="item.id"
      >
        <img :src="item.img.url" :alt="item.title" />
        <MyTitle type="h2" class="-default" :label="item.title" />
         <p class="infoCard__text">{{ item.text }}</p>
      </div>
    </div>
  </div>
</template>


 <style lang="scss" >
.infoCard {
    @include bodyText();
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    align-items: flex-start;
    color: #C5C5C5;
    font-family: supreme;
    font-size: 16px;
    margin: 0 5%;
    padding-bottom: 20px;
    
  &__title {
    line-height: auto;
    max-width: 226px;
  }
  &__image {
    display: flex;
    flex-direction: column;
    align-items:center;
    justify-content: center;
    padding-bottom: 25px;;
    width: 23%;

  }
  &__text {
    text-align: justify;
    max-width: 220px;
  }
}

.list {
  height: 600px;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.bg-perspective {
  background-size: cover;
  background-image: url(../../assets/images/perspective_grille.svg);
}
</style> 

