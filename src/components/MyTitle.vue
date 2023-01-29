<script>
export default {
  data() {
    return {
      className: `title${this.class}`,
    };
  },
  props: {
    class: String,
    type: String,
    label: String,
  },
};
</script>
<template>
  <h1 v-if="type === 'h1'" :class="className">{{ label }}</h1>
  <h2 v-else-if="type === 'h2'" :class="className">{{ label }}</h2>
</template>

<style lang="scss" scoped>
.title {
  @include title();
  &-enormous {
    font-size: pxToRem(80);
  }
  &-big {
    font-size: pxToRem(30);
  }
  &-default {
    font-size: pxToRem(20);
  }
  &-footer {
    font-size: pxToRem(16);
  }
  &-menu {
    font-size: pxToRem(16);
    padding-right: 22px;
  }
  &-icone {
    padding-right: 20px;
  }
}
</style>
