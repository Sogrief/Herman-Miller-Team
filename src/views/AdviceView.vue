<template>
    <div class="conseils">
    {{page.title.rendered}}
  </div>
  <div v-if="page.content" v-html="page.content.rendered"></div>

</template>

<script>
    import { client } from "@/outils/axios"
export default {
    data() {
        return{
            page:{}
        };
    },

    async created () {
    const response = await client.get(
      import.meta.env.VITE_WP_API_URL + "/wp/v2/pages?slug=conseils&_fields=id,title,content,date,excerpt"
    );
     this.page = response.data[0];
     
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