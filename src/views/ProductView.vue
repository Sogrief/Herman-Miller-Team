<script>
import MyButton from "@/components/MyButton.vue";
import MyTitle from "@/components/MyTitle.vue";
import MyHeader from "@/components/MyHeader.vue";
import MyText from "@/components/MyText.vue";
import MyInfoCard from "@/components/MyInfoCard.vue";
import MyCheckbox from "@/components/MyCheckbox.vue";
import MyFooter from "@/components/MyFooter.vue";
import DefaultLayout from "@/layout/DefaultLayout.vue";

export default {
  components: {
    MyButton,
    MyTitle,
    MyHeader,
    MyText,
    MyInfoCard,
    MyCheckbox,
    MyFooter,
    DefaultLayout,
  },
};
</script>

<template>
  <main>
    <MyHeader />

    <MyFooter />
  </main>
</template>
