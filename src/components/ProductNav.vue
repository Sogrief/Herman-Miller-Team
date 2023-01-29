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
        <div class="specification-link">
          <a href="">
            <MyTitle
              :label="acf.product_technique.technique_link_text"
              type="h3"
              class="-menu"
            />
            <svg
              width="22"
              height="32"
              viewBox="0 0 22 32"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M0.388203 24.7V31.3L19.4682 20.68L13.5282 17.38L0.388203 24.7ZM0.388203 0.7V7.3L21.9882 19.3V12.7L0.388203 0.7Z"
                fill="#01E6B6"
              />
            </svg>
          </a>
        </div>
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
            <!-- Voir pour faire sous forme de liste -->
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
  margin-top: 90px;
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
    position: relative;
    display: flex;
    &-img {
      display: flex;
      flex-direction: column;
      img {
        background-image: url("../../assets/images/grille_produit.svg");
        background-size: 944px 696px;
        background-position: center;
      }
      a {
        margin-top: 5vh;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 15px;
      }
    }
    &-info {
      position: absolute;
      left: 57vw;
      top: 13vh;
    }
    &-card {
      z-index: 2;
      margin-bottom: 60px;
      p {
        width: 330px;
      }
    }
  }
}
</style>
