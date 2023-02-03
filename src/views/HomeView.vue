<script>
import {client} from '@/outils/axios.js';
import MyButton from "@/components/MyButton.vue";
import MyTitle from "@/components/MyTitle.vue";
import MyHeader from "@/components/MyHeader.vue";
import MyText from "@/components/MyText.vue";
import MyInfo from "@/components/MyInfo.vue";
import MyCheckbox from "@/components/MyCheckbox.vue";
import MyFooter from "@/components/MyFooter.vue";
import DefaultLayout from "@/layout/DefaultLayout.vue";

export default {
  components: {
    MyButton,
    MyTitle,
    MyHeader,
    MyText,
    MyInfo,
    MyCheckbox,
    MyFooter,
    DefaultLayout,
  },

  data(){
    return {
      front: {},
    }
  },

  async mounted() {
    const response = await client.get(
      import.meta.env.VITE_WP_API_URL +
        "/wp/v2/pages/11"
    );
    this.front = response.data;
  },
};
</script>

<template>
  <!-- <MyTitle />
    <MyTitle size="big" label="grand titre h1" />
    <MyTitle size="tiny" type="h2" label="petit titre h2" />
    <MyButton type="quantite" label="+" />
    <MyButton type="precedent" label="+" />
    <MyButton type="suivant" label="+" />
    <MyButton label="+" />
    <MyHeader />
   <MyCheckbox />
     <MyTitle size="-little" label="test" />
     <MyText type="lien" label="blabla" size="body" />  -->
     <DefaultLayout>
        <template v-slot:header>
          <MyHeader />
        </template>
        <main class="accueil">
          <div v-if="front.content" v-html="front.content.rendered"></div>
          <!--<MyTitle size="-enormous" label="Aeron" type="h1" />
          <MyButton class="decouvrirAeron" label="Découvrir" />-->
          <MyInfo v-if="front.acf" :acf="front.acf" />
          
        </main>
        <template v-slot:footer>
          <MyFooter />
        </template>
      </DefaultLayout>
</template>

<style lang="scss">
.accueil{
h2,h1{text-align: center;}

  .imgEntete{
    width:90vw;
    margin-left:5vw;

    img{
      width: 100%;
    }
  }

  .wp-block-gallery-4, .wp-block-gallery{
    display: flex;
    justify-content: center;
    margin-bottom: pxToRem(175);
    figure{
      width:pxToRem(300);
      img{
        width:100%;
        height:auto;
      }

      figcaption{
        @include bodyText();
        text-align: center;
      }
    }
  }

  .wp-block-media-text__media{
  margin:auto;
  }

  .wp-block-media-text{
      width:50vw;
      margin:auto;
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
    }

    .wp-block-buttons{
      display: flex;
      justify-content: center;
    }
  .wp-block-group{
    display: flex;
    justify-content: center;
  }

  .wp-block-button{
    margin:auto;
    a{
      color: $mainColor !important;
      background-color: $backgroundColor;
      border: 1px solid $mainColor;
      width: auto;
      padding: pxToRem(5) pxToRem(30);
      @include bodyText();
    }

    &:hover {
      cursor:pointer;

      a{
        color: white !important;
      }
    }
  }
}

.decouvrirAeron{
  display: inline;
  text-align: center;
}
</style>
