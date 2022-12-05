<script>
export default{
  data() {
    return {
      className: `title ${this.size}`,
    };
  },
  props: {
    size: String,
    type: String,
    label: String,
  },
};
</script>

<template>
  <h1 :class="className">{{ label }}</h1>
</template>

<style lang="scss" scoped>
@import "./../scss/foundations/variables";
.title {
  font-family: $textFont;
  font-size: 2rem;
  &.-tiny {
    font-size: 1rem;
  }
  &.-big {
    font-size: 3rem;
  }
}
</style>
