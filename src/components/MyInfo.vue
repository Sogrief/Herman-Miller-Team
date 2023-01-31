<script>
import { client } from "@/outils/axios";
import MyTitle from "./MyTitle.vue";
export default {
  components: {
    MyTitle,
  },
  data() {
    return {
      infos: [],
    };
  },
   async mounted() {
     const response = await client.get(
       import.meta.env.VITE_WP_API_URL +
         "/wp/v2/pages/11"
     );
     this.infos =  response.data;
     console.log(response.data)
   },
}

</script>
<template>
  <div class="bg-perspective">
    <div class=" infoCard" v-if="acf.infos">
       <div class="infoCard__image"
       v-for="item in acf.infos"
       :key="item.id">
        <img :src="item.img.url" :alt="title" />
        <MyTitle type="h3" class="infoCard__title" :label="item.infos.title" />
      </div>
      <p class="infoCard__text">{{ item.infos.text }}</p>
    </div>
  </div>
</template>




 <style lang="scss" >
.infoCard {
  @include bodyText();
  &__title {
    line-height: auto;
    max-width: 226px;
  }
  &__image {
    display: flex;
    justify-content: center;
    padding-bottom: 24px;

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

