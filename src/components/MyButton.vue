<script>
export default {
  props: {
    label: String,
    href: String,
    type: String,
  },
};
</script>

<template>
  <a
    v-if="href"
    :href="href"
    :className="this.type === 'secundary' ? 'button-secundary' : 'button'"
    >{{ label }}</a
  >
  <button
    v-else
    :className="this.type === 'secundary' ? 'button-secundary' : 'button'"
  >
    {{ label }}
  </button>
</template>

<style lang="scss" scoped>
@import "./../scss/foundations/variables";
$bg: $primaryColor;
$color: white;
.button {
  padding: 1rem;
  display: inline-block;
  background-color: $bg;
  color: $color;
  text-decoration: none;
  border: 1px solid;
  border-radius: 5px;
  &:hover {
    background-color: $color;
    color: $bg;
  }
}
</style>
