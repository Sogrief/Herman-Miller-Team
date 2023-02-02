<script>
import MyTitle from './MyTitle.vue';
export default {
  data() {
    return {
      active: this.slide[0],
      currentIndex: 1,
    };
  },
    components: {
        MyTitle,
    },
    props: {
    slide: {
      type: Array,
      default: () => [],
    },
 },
 methods: {
    previous() {
      this.currentIndex = (this.currentIndex - 1 + this.acf.product_ergonomy.length) % this.acf.product_ergonomy.length;
    },
    next() {
      this.currentIndex = (this.currentIndex + 1) % this.acf.product_ergonomy.length;
      console.log(this.currentIndex);
    },
    
  }
}
</script>

<template>
    <div class="ergonomie" v-if="slide">
      <!-- <div class="ergonomie-card active" v-if="active">
        <MyTitle :label="active.ergonomy_title" type="h2" class="-default" />
        <img :src="active.ergonomy_image.url" />
         A voir pour le carousel et l'importation des gifs
        <p class="caption">{{ active.ergonomy_text }}</p>
      </div> -->
      <div
        class="ergonomie-card"
        v-if="active"
        v-for="item in slide"
        :key="index"
        :class="{ 'active':  currentIndex === active.id }"
      >
        <MyTitle :label="item.ergonomy_title" type="h2" class="-default" />
        <img :src="item.ergonomy_image.url" />
        <!-- A voir pour le carousel et l'importation des gifs -->
        <p class="caption">{{ item.ergonomy_text }}</p>
      </div>
      <button @click="previous" class="ergonomie-button prev">
        <svg
          width="12"
          height="22"
          viewBox="0 0 12 22"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M11.8952 0.0500491L12.6764 0.801846L2.24719 11.0395L12.6985 21.2983L11.9171 22.05L0.698488 11.0392L11.8952 0.0500491Z"
            fill="#01E6B6"
          />
        </svg>
      </button>
      <button @click="next" class="ergonomie-button next">
        <svg
          width="12"
          height="22"
          viewBox="0 0 12 22"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M0.803288 22L0.022106 21.2482L10.4513 11.0105L0 0.751796L0.781379 0L12 11.0108L0.803288 22Z"
            fill="#01E6B6"
          />
        </svg>
      </button>
    </div>
</template>

<style lang="scss">
.ergonomie {
  position: relative;
  height: 100vh;
  &-card {
    width: 100%;
    height: 100vh;
    display: block;
    transition: opacity 0.5s ease-in-out;
    position: absolute;
    object-fit: cover;
    opacity: 0;
    &.active{
      opacity: 1;
    }
    img {
      width: 90vw;
    }
    .title-default, .caption{
      position: absolute;
    }
    .title-default{
      top: 22px;
      left: 33px;
    }
    .caption{
      bottom: 50px;
      width: 350px;
      right: 30px;
    }
  }
  &-button {
    background-color: transparent;
    border: none;
    position: absolute;
    cursor: pointer;
    top: 50%;
    &.next{
      right: 10px;
    }
    &.prev{
      left: 10px;
    }
  }
}

</style>