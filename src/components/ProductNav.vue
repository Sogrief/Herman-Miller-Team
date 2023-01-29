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

  <div class="technique" v-if="acf.product_technique">
    <div class="specification">
      <div class="specification-img">
        <img :src="acf.product_technique.technique_image.url" />
        <a href="">
          <MyTitle
            :label="acf.product_technique.technique_link_text"
            type="h3"
            class="-default"
        /></a>
      </div>
      <div
        class="specification-info"
        v-if="acf.product_technique.product_specification"
      >
        <div
          class="specification-card"
          v-for="item in acf.product_technique.product_specification"
          :key="item.id"
        >
          <MyTitle
            :label="item.specification_title"
            type="h3"
            class="-default"
          />
          <p>
            {{ item.specification_text }}
          </p>
        </div>
      </div>
    </div>

    <div class="materiaux" v-if="acf.product_technique.product_materials">
      <MyTitle label="Matériaux" type="h2" class="-title titre" />
      <div
        class="materiaux-card"
        v-for="item in acf.product_technique.product_materials"
        :key="item.id"
      >
        <img :src="item.materials_image.url" />
        <MyTitle :label="item.materials_title" type="h3" class="-default" />
        <p>{{ item.materials_text }}</p>
      </div>
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
  grid-template-rows: 20vh 1fr 1fr;
  margin-top: 50px;
  grid-gap: 0;
  margin-left: 13vw;
  & > .titre {
    background-image: url(../../assets/images/encart_titre.svg);
    background-repeat: no-repeat;
    padding: 15px 25px;
    grid-column: 1 / span 3;
  }
  &-card {
    margin-bottom: 35px;
    img {
      width: 182px;
      height: 182px;
    }
    p {
      width: 182px;
    }
    &:nth-of-type(5) > h3 {
      width: 180px;
      line-height: 27px;
    }
  }
}

.product_nav {
  display: flex;
  gap: 155px;
  justify-content: center;
}

.technique {
  .specification {
    display: flex;
    &-img {
      background-image: url('../../assets/images/grille_produit.svg');
    }
  }
}
</style>
