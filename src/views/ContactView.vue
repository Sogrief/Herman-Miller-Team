<template>
  <DefaultLayout>
  <template v-slot:header>
  <MyHeader />
  </template>
  
    <div class="contact">
    </div>
    <div class="container" v-if="page.content" v-html="page.content.rendered"></div>
  
  <template v-slot:footer>
      <MyFooter />
  </template>
  </DefaultLayout>
  
</template>

<script>
import { client } from "@/outils/axios";
import MyHeader from "@/components/MyHeader.vue";
import MyFooter from "@/components/MyFooter.vue";
import DefaultLayout from "@/layout/DefaultLayout.vue";

export default {
  data() {
    return {
      page: {},
    };
  },

  components: { 
    MyHeader,
    MyFooter,
    DefaultLayout},

  async created() {
    const response = await client.get(
      import.meta.env.VITE_WP_API_URL +
        "/wp/v2/pages?slug=contact&_fields=id,title,content,date,excerpt"
    );
    this.page = response.data[0];
  },
};
</script>

<style lang="scss">
.wpcf7{
  width:50vw;

  input{
    border:1px solid $mainColor;
    background-color: $backgroundColor;
    padding:pxToRem(7) pxToRem(10) pxToRem(7) pxToRem(10);
    color:white;
    
  }

  input:not(.wpcf7-submit), textarea
  {
    width:100%;
  }
  

  textarea{
    border:1px solid $mainColor;
    background-color: $backgroundColor;
    resize: none;
  }

  .wpcf7-submit
  {
    padding: pxToRem(5) pxToRem(30);
    color:$mainColor;

    &:hover {
      color: white;
      cursor:pointer;
    }
  }
}

.container{
  display: flex;
  flex-direction: column;
  align-items: center;
  width:unset;
  max-width:60vw;
  margin-left:20vw;
  margin-bottom: pxToRem(150);
  margin-top:pxToRem(100);
}

@media screen and (max-width: map-get($breakpoints, "tablet-down")) {
  .container{
    width:80vw;
    margin-left:10vw;
  }

  .wpcf7{
    width:80vw;
    margin-left:10vw;
  }
}

</style>