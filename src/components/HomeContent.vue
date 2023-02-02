<template>
    <div v-if="page.content" v-html="page.content.rendered"></div>
</template>

<script>
import { client } from "@/outils/axios";



export default {
  data() {
    return {
      page: {},
    };
  },

  async created() {
    const response = await client.get(
      import.meta.env.VITE_WP_API_URL +
        "/wp/v2/pages?slug=accueil&_fields=id,title,content,date,excerpt"
    );
    this.page = response.data[0];
  },
};
</script>


<style>
.imgEntete>img{
    width: 100%;
}
</style>