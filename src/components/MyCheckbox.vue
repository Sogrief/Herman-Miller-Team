<script>
</script>

<template>
  <input type="checkbox" id="checkbox" />
  <label for="checkbox"></label>
</template>

<style lang="scss" scoped>
#checkbox {
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
</style>
