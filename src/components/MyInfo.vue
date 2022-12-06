<script>
export default {
  props: {
    title: String,
    srcImage: String,
    content: String,
  },
};
</script>
<template>
  <div class="infoCard">
    <div class="infoCard__image">
      <img :src="srcImage" :alt="title" />
    </div>
    <p class="infoCard__title">{{ title }}</p>
    <p class="infoCard__content">{{ content }}</p>
  </div>
</template>

<style lang="scss" scoped>
.infoCard {
  max-width: 200px;
  border-radius: 5px;
  padding: 1rem;
}
</style>
