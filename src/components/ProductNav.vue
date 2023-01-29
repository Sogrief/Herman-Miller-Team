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
  <nav class="product_nav">
    <MyTitle type="h2" class="-default" label="Points forts" />
    <MyTitle type="h2" class="-default" label="Ergonomie" />
    <MyTitle type="h2" class="-default" label="Volet technique" />
    <!-- A voir comment récupérer les titres des ACF -->
  </nav>

  <div class="pointforts" v-if="acf.product_advantage">
    <div
      class="pointforts-card"
      v-for="item in acf.product_advantage"
      :key="item.id"
    >
      <img :src="item.advantage_image.url" />
      <p>{{ item.advantage_text }}</p>
    </div>
  </div>

  <div class="ergonomie" v-if="acf.product_ergonomy">
    <div
      class="ergonomie-card"
      v-for="item in acf.product_ergonomy"
      :key="item.id"
    >
      <MyTitle :label="item.ergonomy_title" type="h2" class="-default" />
      <img :src="item.ergonomy_image.url" />
      <!-- A voir pour le carousel et l'importation des gifs -->
      <p>{{ item.ergonomy_text }}</p>
    </div>
  </div>

  <div class="specification" v-if="acf.product_specification">
    <div
      class="specification-card"
      v-for="item in acf.product_specification"
      :key="item.id"
    >
      <MyTitle :label="item.specification_title" type="h2" class="-default" />
      <p>{{ item.specification_text }}</p>
    </div>
  </div>

  <div class="materiaux" v-if="acf.product_materials">
    <MyTitle label="Matériaux" type="h2" class="-default" />
    <div
      class="materiaux-card"
      v-for="item in acf.product_materials"
      :key="item.id"
    >
      <img :src="item.materials_image.url" />
      <MyTitle :label="item.materials_title" type="h2" class="-default" />
      <p>{{ item.materials_text }}</p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
p {
  @include bodyText();
}
.pointforts {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-row-gap: 35px;
  margin-top: 120px;
  margin-left: 130px;
  &-card {
    display: flex;
    align-items: center;
    gap: 40px;
    p {
      max-width: 270px;
    }
  }
}

.materiaux {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  margin-top: 50px;
  grid-gap: 0;
  margin-left: 13vw;
  &-card {
    img {
      width: 182px;
      height: 182px;
    }
    p {
      max-width: 182px;
    }
  }
}

.product_nav{
  display: flex;
  gap: 155px;
  justify-content: center;
}
</style>
