<script>
import MyButton from "./../components/MyButton.vue";
import MyTitle from "./../components/MyTitle.vue";
import MyHeader from "./../components/MyHeader.vue";
import MyText from "./../components/MyText.vue";
export default {
  components: {
    MyButton,
    MyTitle,
    MyHeader,
    MyText,
  },
};
</script>

<template>
  <main>
    <MyHeader />
    <MyTitle size="-little" label="test" />
    <MyText size="-body" label="blabla" />
    <MyText size="-liens" label="blabla" />

  </main>
</template>
