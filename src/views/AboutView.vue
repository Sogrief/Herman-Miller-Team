<template>
  
  <MyHeader />
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
    margin: 0 35vh;
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
    font-size: 1.25em;
  }
  .gapAbout{
    gap: 58px;
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
    display: flex;
    justify-content: center;
    transform: skew(-26deg);
  }


  .containerH h1 {
    transform: skew(26deg);
    margin : 15px;
  }


    .greenBlock {
    background-color: #01E6B6;
    color: #2b2b2b;
    padding: 50px;
    position: relative;
    left: 20%;
    width: 477px;
  }

  .blockValeur{
    background-image: url('/assets/images/Encart _fleche_.png');
    background-repeat: no-repeat;
    background-position-x: 20%;
    background-position-y: 94%;
    
  }
  
  .blockValeur::before{
    background-image: url('/assets/images/Fond_pointillé.png');
    content: "";
    position: absolute;
    top: 119%;
    width: 53%;
    height: 66%;
    z-index: -1;
  }

.imgApropos{
  top: 0px;
  position: relative;
  right: 188px;
  z-index: -1;
  }

  .aProposBlock{
      max-width: 53%;
      position: relative;
      left: 50%;
  }
  .aProposText{
      margin: 0;
  }

  .citation{
  background-image: url('/assets/images/guillemet.svg');
  background-size: 10px;
  background-repeat: no-repeat;
  margin:2px;   
  }

  .contourApropos{
    background-image: url('/assets/images/encartAp.svg');
    background-size: 367px;
    background-repeat: no-repeat;
    background-position: top right;
  }
}

</style>
