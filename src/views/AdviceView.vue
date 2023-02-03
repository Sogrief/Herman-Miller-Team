<template>
  <MyHeader />
  <div v-if="page.content" v-html="page.content.rendered"></div>
</template>

<script>
import { client } from "@/outils/axios";
import MyTitle from "@/components/MyTitle.vue";
import MyHeader from "@/components/MyHeader.vue";
import MyText from "@/components/MyText.vue";

export default {
  components: {
    MyTitle,
    MyHeader,
    MyText,
  },
  data() {
    return {
      page: {},
    };
  },

  async created() {
    const response = await client.get(
      import.meta.env.VITE_WP_API_URL +
        "/wp/v2/pages?slug=conseils&_fields=id,title,content,date,excerpt"
    );
    this.page = response.data[0];
  },
};
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}

.wp-block-gallery {
  display: grid;
  grid-template-columns: 21.3% 24% 24% 24%;
  margin-bottom: 130px;
}

.wp-block-image:nth-child(0n + 2) {
  margin-top: -53px;
}

.wp-block-image:nth-child(0n + 3) {
  margin-top: -10px;
}

.wp-block-image:nth-child(0n + 4) {
  margin-top: 34px;
}

.wp-block-image:nth-child(0n + 5) {
  margin-top: -88px;
}

.titre {
  margin-bottom: 138px;
  display: flex;
  justify-content: center;
}

.titre h2 {
  height: 100px;
  width: 450px;
  background-image: url(/assets/images/encarts-1.svg);
  background-repeat: no-repeat;
  padding-top: 35px;
  padding-left: 50px;
}

.texte1 {
  background-image: url(/assets/images/encarts-3.svg);
  background-repeat: no-repeat;
  width: 456px;
  height: 356px;
  margin-left: 40px;
}

.texte2 {
  background-image: url(/assets/images/encarts-4.svg);
  background-repeat: no-repeat;
  width: 456px;
  height: 356px;
  margin-right: 40px;
}

.texte2 p {
  width: 371px;
  height: 165px;
}

.texte3 p {
  width: 412px;
  height: 256px;
}

.texte3 {
  background-image: url(/assets/images/encarts-5.svg);
  background-repeat: no-repeat;
  width: 456px;
  height: 380px;
  margin-left: 40px;
}

.texte1 p {
  width: 417px;
  height: 91px;
}

.titre2 h2 {
  height: 100px;
  width: 450px;
  background-image: url(/assets/images/encarts-2.svg);
  background-repeat: no-repeat;
  padding-top: 35px;
  padding-left: 70px;
}

.titre2 {
  display: flex;
  justify-content: center;
}

.bloc {
  display: flex;
  justify-content: center;
}

.encadre {
  padding: 20px;
}
</style>
