<script>
import MyTitle from "./MyTitle.vue";
import ProductAdvantage from "./ProductAdvantage.vue";
import ProductErgonomy from "./ProductErgonomy.vue";
import ProductTechnique from "./ProductTechnique.vue";
import MyText from "./MyText.vue";
export default {
  components: {
    MyTitle,
    MyText,
    ProductAdvantage,
    ProductErgonomy,
    ProductTechnique,
  },
  props: {
    acf: {
      type: Array,
      default: () => [],
    },
    image:{
      type: Array,
      defautl: () => []
    }
  },
  data() {
    return {
      currentIndex: 0,
      active: this.acf.product_ergonomy[0]
    };
  },
  methods: {
    prev() {
      if (this.currentIndex === 0) {
        this.active[currentIndex].style.display = "none";
        this.active = this.acf.product_ergonomy[this.currentIndex]
        this.active[currentIndex].style.display = "block";

      } else {
        this.currentIndex--;
      }
    },
    next() {
      if (this.currentIndex === this.acf.product_ergonomy.length - 1) {
        this.currentIndex = 0;
      } else {
        this.currentIndex++;
      }
    },
  },

  mounted() {
  var acc = document.querySelectorAll('.nav_title');
  var i;

  for (i = 0; i < acc.length; i++) {
    acc[i].addEventListener("click", function() {
      this.classList.toggle("active");
      var panel = this.nextElementSibling;
      if (panel.style.display) {
        panel.style.display = null;
      } else {
        panel.style.display = "block";
      } 
    });
  }
}
};
</script>

<template>
<nav class="product_nav">
  <div class="nav_advantage">
    <div class="nav_title">
      <MyTitle type="h2" class="-default" label="Points forts" />
      <img src="../../assets/images/arrow_nav.svg" alt="">
    </div>
    <div class="nav_text">
      <ProductAdvantage :acf="acf" />
    </div>
    
  </div>
  <div class="nav_ergonomy">
    <div class="nav_title">
      <MyTitle type="h2" class="-default" label="Ergonomie" />
      <img src="../../assets/images/arrow_nav.svg" alt="">
    </div>
    <div class="nav_text">
      <ProductErgonomy :slide="acf.product_ergonomy" />
    </div>
  </div>
  <div class="nav_technique">
    <div class="nav_title">
      <MyTitle type="h2" class="-default" label="Volet technique" />
      <img src="../../assets/images/arrow_nav.svg" alt="">
    </div>
    <div class="nav_text">
      <ProductTechnique :acf="acf" />
    </div>
  </div>
</nav> 

<div class="product_link" v-if="acf.product_link">
  <div class="link" v-for="item in acf.product_link" :key="item.id">
    <img :src="item.link_image.url">
      <a class="link_title" href="">
      <MyText size="menu" type="lien" :label="item.link_text" />
      <svg width="19" height="26" viewBox="0 0 19 26" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0.156592 20.25V25.75L16.0566 16.9L11.1066 14.15L0.156592 20.25ZM0.156592 0.25V5.75L18.1566 15.75V10.25L0.156592 0.25Z" fill="#01E6B6"/>
      </svg>
    </a>
  </div>
</div>
</template>

<style lang="scss" scoped>
p {
  @include bodyText();
}

.product_nav {
  margin-left: 40px;
  margin-top: 40px;
  .nav_title{
    width: 50px;
    display: flex;
    align-items: center;
    gap: 20px;
    border-bottom: solid 1px $bodyText;
    cursor: pointer;
  }
  .nav_text{
    display: none;
  }
}

.link{
  display: flex;
  align-items: flex-end;
  &_title{
    display: flex;
    align-items: center;
    gap: 10px;
  }
  img{
    padding-left: 70px;
  }
}

.panel {
  display: block;
  transition: max-height 0.2s ease-out;
}
</style>
