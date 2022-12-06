<script>
import MyTitle from './MyTitle.vue'
export default {
  props: {
    title: String,
    srcImage: String,
    label: String,
  },
  components: {
    MyTitle,
  }
};

</script>
<template>
  <div class="infoCard">
    <div class="infoCard__image">
      <img :src="srcImage" :alt="title" />
    </div>
    <MyTitle class="title" size="-default" type="h2" v-bind:label="title"/>
    <p class="infoCard">{{ label }}</p>
  </div>
</template>

<style lang="scss" scoped>
.infoCard {
  max-width: 200px;
  border-radius: 5px;
  padding: 1rem;
}
</style>
