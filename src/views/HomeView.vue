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
      page:{}
    }
  },

  async created(){
    const resp = await client.get(
      import.meta.env.VITE_WP_API_URL +
        "/wp/v2/pages?slug=accueil&_fields=id,title,content,date,excerpt"
    );

    this.page = resp.data;
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
        <main>
          <MyTitle size="-enormous" label="Aeron" type="h1" />
          <MyButton label="Découvrir" />
          <MyInfo v-if="front.acf" :acf="front.acf" />

          <div v-if="page.content" v-html="page.content.rendered"></div>
        </main>
        <template v-slot:footer>
          <MyFooter />
        </template>
      </DefaultLayout>
</template>
