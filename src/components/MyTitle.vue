<script>
export default {
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
<h2 :class="className">{{ label }}</h2> 
</template>

<style lang="scss" scoped>
.title {

  font-family: $textFontFamily;
  font-size: 2rem;
  &.-tiny {
    font-size: 1rem;
  }

  @include title();

  &.-enormous {
    // font-size: pxToRem(14);
    font-size: pxToRem(85);
  }
  &.-big {
    // font-size: pxToRem(14);
    font-size: pxToRem(35);
  }
  &.-default {
    // font-size: pxToRem(14);
    font-size: pxToRem(25);
  }
  &.-footer {
    font-size: pxToRem(16);
  }
  &.-menu {
    font-size: pxToRem(16);
    padding-right: 22px;
  }
  &.-icone {
    padding-right: 20px;
  }
}
</style>
