<script>
import MyTitle from "./MyTitle.vue";
import MyText from "./MyText.vue";
export default {
  components: {
    MyTitle,
    MyText,
  },
  props: {
    meta_data: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<template>
  <div>
  </div>
  {{ meta_data[3].value }}
</template>

<style lang="scss" scoped>
p {
  @include bodyText();
}
.pointforts {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-row-gap: 35px;
  margin-top: 120px;
  margin-left: 130px;
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
  grid-template-rows: 1fr 1fr;
  margin-top: 50px;
  grid-gap: 0;
  margin-left: 13vw;
  &-card {
    img {
      width: 182px;
      height: 182px;
    }
    p {
      max-width: 182px;
    }
  }
}
</style>
