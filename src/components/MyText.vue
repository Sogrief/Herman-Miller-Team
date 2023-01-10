<script>
export default {
  data() {
    return {
      className: `${this.type} -${this.size}`,
    };
  },
  props: {
    size: String,
    type: String,
    label: String,
    href: String,
  },
};
</script>

<template>
  <p v-if="type === 'text'" :class="className" :size="size">
    {{ label }}
  </p>
  <h3 v-else-if="type === 'h3'" :class="className" :size="size">{{ label }}</h3>
  <a v-else:href="href" :class="className" :size="size">
    {{ label }}
  </a>
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
  &.-labelForm {
    color: $bodyText;
    font-size: pxToRem(12);
    font-family: $textFontFamily;
  }
}
.titre{
  
}
.lien {
  cursor: pointer;
  &.-body {
    font-size: pxToRem(14);
    font-family: $textFontFamily;
    color: $bodyText;
  }
  &.-menu {
    font-size: pxToRem(16);
    font-family: $titleFontFamily;
    color: white;
  }
  &.-footer {
    font-size: pxToRem(12);
    font-family: $textFontFamily;
    color: $bodyText;
  }
  &:hover {
    color: $mainColor;
    text-decoration: underline;
  }
}
</style>
