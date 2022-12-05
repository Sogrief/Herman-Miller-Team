<script>
export default {
  data() {
    return {
      className: `button ${this.type === "secondary" ? "-secondary" : ""}`,
    };
  },
  props: {
    label: String,
    type: String,
    href: String,
  },
};
</script>

<template>
  <a v-if="href" :href="href" :class="className">
    {{ label }}
  </a>
  <button v-else :class="className">
    {{ label }}
  </button>

  <a v-if="href" :href="href" :class="colorCheck">
    {{ label }}
  </a>
  <button v-else :class="colorCheck">
    {{ label }}
  </button>

  <div class="colorCheck">
    <input type="checkbox" id="checkbox" />
    <label for="checkbox"></label>
  </div>
</template>

<style lang="scss" scoped>
@import "./../scss/foundations/variables";

//bouton classique
.button {
  color: $mainColor;
  border: 1px solid $mainColor;
  width: auto;
  padding: pxToRem(5) pxToRem(30);
  &:hover {
    color: white;
  }

  //boutton avec flèche
  &.-suivant {
    &::after {
      border-style: solid;
      border-width: 0.12em 0.12em 0 0;
      content: "";
      display: inline-block;
      height: pxToRem(6);
      left: pxToRem(3);
      position: relative;
      transform: rotate(45deg);
      vertical-align: center;
      width: pxToRem(6);
    }
  }

  &.-precedent {
    &::before {
      border-style: solid;
      border-width: 0.12em 0.12em 0 0;
      content: "";
      display: inline-block;
      height: pxToRem(6);
      right: pxToRem(3);
      position: relative;
      transform: rotate(-135deg);
      vertical-align: center;
      width: pxToRem(6);
    }
  }
}

button.quantité {
  width: 20px;
  height: 20px;
  background: transparent;
  color: $mainColor;
  border: 1px solid $mainColor;

  &:hover {
    background: $mainColor;
    color: #2b2b2b;
    border: none;
  }
}

//colorCheck
.colorCheck {
  input[type="checkbox"] {
    display: none;

    &:checked + label {
      background-color: transparent;
    }

    &:checked + label:before {
      opacity: 1;
    }
    &:checked + label:after {
      opacity: 1;
    }
  }

  label {
    background-color: $bodyText;
    cursor: pointer;
    height: 20px;
    width: 20px;
    position: absolute;
    display: flex;
    &:before {
      height: 15px;
      width: 15px;
      opacity: 0;
      content: "";
      position: absolute;
      top: 4.5px;
      left: 4.5px;
      background-color: $bodyText;
    }
    &:after {
      border: 2px solid $mainColor;
      width: 20px;
      height: 20px;
      position: absolute;
      content: "";
      opacity: 0;
      border-style: dashed;
    }
  }
}
</style>
