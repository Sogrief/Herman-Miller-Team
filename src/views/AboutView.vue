<template>
  

  <div class="about" v-if="page.content" v-html="page.content.rendered"></div>


</template>


<script>
import { client } from "@/outils/axios";
import MyTitle from "@/components/MyTitle.vue";
import MyHeader from "@/components/MyHeader.vue";
import MyText from "@/components/MyText.vue";

export default{
  components:{
    MyTitle,
    MyHeader,
    MyText,
  },
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
    margin: 0 125px;
  }
  .imgText{
    display: flex;
    align-items: center;
  }

  .imgText>div>p{
    text-align: justify;
  }
  
  blockquote>p{
    text-align: center;
  }
  .gapAbout{
    gap: 140px;
  }
  
  h1,h2{
    text-align :center;
  }

 /* contour incliné */
  .containerH>div{
    border: 1px #01E6B6 solid;
    width : 35%;
  }

  .containerH {
    transform: skew(-26deg);
  }


  .containerH h1 {
    transform: skew(26deg);
    margin : 15px;
  }



}
</style>
