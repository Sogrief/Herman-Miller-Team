<script>
export default {
    props: {
    acf: {
      type: Array,
      default: () => [],
    },
 }
}
</script>

<template>
    <div class="pointforts" v-if="acf.product_advantage">
        <div
        class="pointforts-card"
        v-for="item in acf.product_advantage"
        :key="item.id"
        >
        <img :src="item.advantage_image.url" />
        <p>{{ item.advantage_text }}</p>
        </div>
  </div>
</template>

<style lang="scss" scoped>
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
</style>