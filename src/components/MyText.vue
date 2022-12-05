<script>
export default {
  data() {
    return {
      className: `text ${this.size}`,
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
  <p :class="className" :size="size">{{ label }}</p>
</template>

<style lang="scss" scoped>
@font-face {
  font-family: supreme;
  src: url("../../assets/fonts/SUPREME-REGULAR.OTF");
}
@font-face {
  font-family: deserta;
  src: url("../../assets/fonts/DESERTA.OTF");
}
@font-face {
  font-family: anurati;
  src: url("../../assets/fonts/ANURATI-REGULAR.OTF");
}

.text {
  &.-body {
    color: $bodyText;
    font-size: pxToRem(14);
    font-family: $textFontFamily;
  }
  &.-labelForm {
    color: $bodyText;
    font-size: pxToRem(12);
    font-family: $textFontFamily;
  }
  &.-liens {
    color: $bodyText;
    font-size: pxToRem(12);
    font-family: $textFontFamily;
    &:hover {
      color: $mainColor;
      text-decoration: underline;
    }
  }
}
</style>
