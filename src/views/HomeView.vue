<script>
import {client} from '@/outils/axios.js';
import MyButton from "@/components/MyButton.vue";
import MyTitle from "@/components/MyTitle.vue";
import MyHeader from "@/components/MyHeader.vue";
import MyText from "@/components/MyText.vue";
import MyInfoCard from "@/components/MyInfoCard.vue";
import MyCheckbox from "@/components/MyCheckbox.vue";
import MyFooter from "@/components/MyFooter.vue";
import DefaultLayout from "@/layout/DefaultLayout.vue";

export default {
  components: {
    MyButton,
    MyTitle,
    MyHeader,
    MyText,
    MyInfoCard,
    MyCheckbox,
    MyFooter,
    DefaultLayout,
  },

// On récupère les produits de Woocommerce avec le lien récupérer dans Postman
  async mounted() {
    const response =  await client.get('http://localhost/herman/wp-json/wc/v3/products')
    this.products = response.data
  },

  
  data () {
    return{
      products : []
    }
  },
};
</script>

<template>
  <main>
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
    <MyText type="lien" label="blabla" size="body" /> 
     -->

    <DefaultLayout>
      <template v-slot:header>
        <MyHeader />
      </template>
      <MyTitle size="-enormous" label="Aeron" type="h1" />
      <MyButton label="Découvrir" />
      <MyInfoCard />
      <template v-slot:footer>

        <MyFooter />
      </template>
    </DefaultLayout>
  </main>
</template>
