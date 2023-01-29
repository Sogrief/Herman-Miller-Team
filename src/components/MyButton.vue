<script>
export default {
  data() {
    return {
      className: `button -${this.type}`,
    };
  },
  props: {
    label: String,
    type: String,
  },
};
</script>

<template>
  <button :class="className">
    {{ label }}
  </button>
</template>

<style lang="scss" scoped>
@import "./../scss/foundations/variables";

//bouton classique
.button {
  color: $mainColor;
  background-color: $backgroundColor;
  border: 1px solid $mainColor;
  width: auto;
  padding: pxToRem(5) pxToRem(30);
  &:hover {
    color: white;
    cursor:pointer;
  }
  //boutton avec flèche
  &.-suivant {
    &::after {
      @include button();
      transform: rotate(45deg);
    }
  }

  &.-precedent {
    &::before {
      @include button();
      transform: rotate(-135deg);
    }
  }
  &.-quantite {
    width: 20px;
    height: 20px;
    background: transparent;
    color: $mainColor;
    padding: 0;
    border: 1px solid $mainColor;
    &:hover {
      background: $mainColor;
      color: #2b2b2b;
      border: none;
    }
  }

  &.-filtre.actif{
    background-color: $mainColor;
    color:$backgroundColor;

    &:hover{
      color:white;
    }
  }
}
</style>
