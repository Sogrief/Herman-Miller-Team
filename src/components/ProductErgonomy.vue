<script>
import MyTitle from './MyTitle.vue';
import { RouterLink } from 'vue-router';
export default {
  data() {
    return {
      currentIndex: 0
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
  prev() {
    if (this.currentIndex === 0) {
      this.currentIndex = this.slide.length - 1;
      return;
    }
    this.currentIndex--;
  },
    next() {
      if (this.currentIndex === this.slide.length - 1) {
        this.currentIndex = 0;
        return;
      }
      this.currentIndex++;
    }
  }
}
</script>

<template>
  <div class="slider">
    <div class="ergonomie" v-if="slide">
      <div
        class="ergonomie-card"
        v-for=" (item, index) in slide"
        :key="index"
        :style="{ transform: 'translateX(' + (-100 * currentIndex) + '%)' }"
      >
        <MyTitle :label="item.ergonomy_title" type="h2" class="-default" />
        <img :src="item.ergonomy_image.url" />
        <p class="caption">{{ item.ergonomy_text }}</p>
      </div>
    </div>
    <button @click="prev" class="ergonomie-button prev">
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
  height: 100vh;
  display: flex;
  transition: transform 0.5s ease;
  &-card {
    width: 100%;
    object-fit: cover;
    img {
      width: 90vw;
    }
    .title-default, .caption{
      position: absolute;
    }
    .title-default{
      top: 22px;
      right: 38px;
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
.slider {
  position: relative;
  overflow: hidden;
}


</style>