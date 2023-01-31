<script>
var acc = document.querySelectorAll('.button');
var i;

for (i = 0; i < acc.length; i++) {
  acc[i].addEventListener("click", function() {
    this.classList.toggle("active");
    var panel = this.nextElementSibling;
    if (panel.style.maxHeight) {
      panel.style.maxHeight = null;
    } else {
      panel.style.maxHeight = panel.scrollHeight + "px";
    } 
  });
}
import MyTitle from "./MyTitle.vue";
export default {
  components: {
    MyTitle,
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
};
</script>

<template>
  <nav class="product_nav" v-if="acf.nav_title">
    <div class="nav" v-for="item in acf.nav_title" :key="item.id">
      <button class="button">bla</button>
      <MyTitle type="h2" class="-default" :label="item.title" />
      <img src="../../assets/images/arrow_nav.svg" alt="">
    </div>
  </nav>

  <div class="pointforts panel" v-if="acf.product_advantage">
    <div
      class="pointforts-card"
      v-for="item in acf.product_advantage"
      :key="item.id"
    >
      <img :src="item.advantage_image.url" />
      <p>{{ item.advantage_text }}</p>
    </div>
  </div>

  <div>
    <div class="ergonomie panel" v-if="acf.product_ergonomy">
      <div
        class="ergonomie-card"
        v-for="item in acf.product_ergonomy"
        :key="item.id"
      >
        <MyTitle :label="item.ergonomy_title" type="h2" class="-default" />
        <img :src="item.ergonomy_image.url" />
        <!-- A voir pour le carousel et l'importation des gifs -->
        <p class="caption">{{ item.ergonomy_text }}</p>
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
  </div>

  <div class="technique panel" v-if="acf.product_technique">
    <div class="specification">
      <div class="specification-img">
        <img :src="acf.product_technique.technique_image.url" />
        <div class="specification-link">
          <a href="">
            <MyTitle
              :label="acf.product_technique.technique_link_text"
              type="h3"
              class="-menu"
            />
            <svg
              width="22"
              height="32"
              viewBox="0 0 22 32"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M0.388203 24.7V31.3L19.4682 20.68L13.5282 17.38L0.388203 24.7ZM0.388203 0.7V7.3L21.9882 19.3V12.7L0.388203 0.7Z"
                fill="#01E6B6"
              />
            </svg>
          </a>
        </div>
      </div>
      <div
        class="specification-info"
        v-if="acf.product_technique.product_specification"
      >
        <div
          class="specification-card"
          v-for="item in acf.product_technique.product_specification"
          :key="item.id"
        >
          <MyTitle
            :label="item.specification_title"
            type="h3"
            class="-default"
          />
          <p>
            <!-- Voir pour faire sous forme de liste -->
            {{ item.specification_text }}
          </p>
        </div>
      </div>
    </div>

    <div class="materiaux" v-if="acf.product_technique.product_materials">
      <MyTitle label="Matériaux" type="h2" class="-title titre" />
      <div
        class="materiaux-card"
        v-for="item in acf.product_technique.product_materials"
        :key="item.id"
      >
        <img :src="item.materials_image.url" />
        <MyTitle :label="item.materials_title" type="h3" class="-default" />
        <p>{{ item.materials_text }}</p>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
p {
  @include bodyText();
}
.pointforts {
  background-image: url('../../assets/images/Grille_forts.svg');
  background-size: 100vw;
  display: grid;
  margin-bottom: 60px;
  grid-template-columns: 1fr 1fr;
  grid-row-gap: 35px;
  margin-top: 90px;
  padding-left: 130px;
  &-card {
    display: flex;
    align-items: center;
    gap: 40px;
    p {
      max-width: 270px;
    }
  }
}

.materiaux {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 20vh 1fr 1fr;
  margin-top: 50px;
  grid-gap: 0;
  margin-left: 13vw;
  & > .titre {
    background-image: url(../../assets/images/encart_titre.svg);
    background-repeat: no-repeat;
    padding: 15px 25px;
    grid-column: 1 / span 3;
  }
  &-card {
    margin-bottom: 35px;
    img {
      width: 182px;
      height: 182px;
    }
    p {
      width: 182px;
    }
    &:nth-of-type(5) > h3 {
      width: 180px;
      line-height: 27px;
    }
  }
}

.product_nav {
  display: flex;
  gap: 155px;
  justify-content: center;
  .nav{
    display: flex;
    align-items: center;
    gap: 20px;
    border-bottom: solid 1px $bodyText;
  }
}

.technique {
  .specification {
    position: relative;
    display: flex;
    &-img {
      display: flex;
      flex-direction: column;
      img {
        padding-left: 115px;
        background-image: url("../../assets/images/grille_produit.png");
        background-size: 100% 100%;
        background-position: right top;
      }
      a {
        margin-top: 5vh;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 15px;
      }
    }
    &-info {
      position: absolute;
      left: 57vw;
      top: 13vh;
    }
    &-card {
      z-index: 2;
      margin-bottom: 60px;
      p {
        width: 330px;
        line-height: 1.5;
      }
    }
  }
}

.ergonomie {
  position: relative;
  height: 100vh;
  &-card {
    width: 100%;
    height: 100vh;
    display: block;
    position: absolute;
    object-fit: cover;
    &:not(:first-of-type) {
      opacity: 0;
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
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

.active, .nav:hover {
  background-color: #ccc;
}

.panel {
  padding: 0 18px;
  background-color: white;
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.2s ease-out;
}
</style>
