<template>
    <div class="contact">
    </div>
    <div class="content" v-if="page.content" v-html="page.content.rendered"></div>
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

.content{
  display: flex;
  flex-direction: column;
  align-items: center;
  width:unset;
  max-width:60vw;
  margin-left:20vw;
}

@media screen and (max-width: map-get($breakpoints, "tablet-down")) {
  .content{
    width:80vw;
    margin-left:10vw;
  }

  .wpcf7{
    width:80vw;
    margin-left:10vw;
  }
}

</style>