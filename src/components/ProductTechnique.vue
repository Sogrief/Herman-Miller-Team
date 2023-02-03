<script>
import MyTitle from './MyTitle.vue';
import MyText from './MyText.vue';
export default {
    components: {
        MyTitle,
        MyText,
    },
    props: {
    acf: {
      type: Array,
      default: () => [],
    },
 }
}
</script>

<template>
    <div class="technique" v-if="acf.product_technique">
    <div class="specification">
      <div class="specification-img">
        <img :src="acf.product_technique.technique_image.url" />
        <div class="specification-link">
            <RouterLink :to="`/conseils`" class="specification-link_a">
              <MyText size="menu" type="lien" :label="acf.product_technique.technique_link_text" />
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
            </RouterLink>
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
        <MyTitle :label="item.materials_title" type="h3" class="-default"/>
        <p>{{ item.materials_text }}</p>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.technique {
  .specification {
    position: relative;
    display: flex;
    &-link_a {
        margin-top: 5vh;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 15px;
      }
    &-img {
      display: flex;
      flex-direction: column;
      img {
        padding-left: 115px;
        background-image: url("../../assets/images/grille_produit.png");
        background-size: 100% 100%;
        background-position: right top;
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
        line-height: 1.5;
      }
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
</style>