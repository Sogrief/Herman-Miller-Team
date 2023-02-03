<script>
import MyText from "./../components/MyText.vue";

export default{
  props: 
  {
    type: String,
    for: String,
    name:String,
    label:String,
  },
};
</script>

<template>
    <label :for="for">{{label}}</label>
    <input :type="type" />
</template>
  
<style lang="scss" scoped>
    label
    {
      @include bodyText();
    }

    input
    {
      display:block;
      border:2px solid $mainColor;
      padding:pxToRem(5);
      background-color: transparent;
    }
</style>
  