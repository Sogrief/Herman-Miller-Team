<template>
  <div class="about">
    {{page.title.rendered}}
  </div>
  <div v-if="page.content" v-html="page.content.rendered"></div>


</template>


<script>
import { client } from "@/outils/axios"

export default{
  data() {
    return{
      page:{},
    };
  },

  async created () {
    const response = await client.get(
      import.meta.env.VITE_WP_API_URL + "/wp/v2/pages/5"
    );
     this.page = response.data;
     return data()
   },
}

</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
