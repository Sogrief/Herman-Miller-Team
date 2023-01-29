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
}

</script>

<template>
  <div class=" infoCard" v-if="acf.infos">
     <div class="infoCard__image"
     v-for="item in acf.infos"
     :key="item.id">
      <img :src="item.img.url" :alt="title" />
      <MyTitle type="h3" class="infoCard__title" label="{{ item.infos.title }}" />
    </div>
    <p class="infoCard__text">{{ item.infos.text }}</p>
  </div>
</template>



















// export default {
//   props: {
//     title: String,
//     srcImage: String,
//     label: String,
//   },
//   components: {
//     MyTitle,
//   },
// };
// 
<!-- // <template>
//   <div class=" infoCard">
//     <div class="infoCard__image">
//       <img :src="srcImage" :alt="title" />
//     </div>
//     <MyTitle
//       class="infoCard__title"
//       size="-default"
//       type="h2"
//       v-bind:label="title"
//     />
//     <p class="infoCard__text">{{ label }}</p>
//   </div>
// </template>

/* <style lang="scss" scoped>
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
</style>  -->


