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
@import "../scss/foundations/variables";
.title{
    @include title();
    &.-big{
        // font-size: pxToRem(14);
        font-size : pxTorem(35);
    }
    &.-little{
        font-size : pxTorem(20);
    }
    &.-menu{
        font-style: pxTorem(16);
        text-transform: uppercase;
        padding-right : 22px;
    }
    &.-icone{
        padding-right: 20px;
    }
  }
</style>
