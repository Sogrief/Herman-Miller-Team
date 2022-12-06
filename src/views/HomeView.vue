<script>
import MyButton from "./../components/MyButton.vue";
import MyTitle from "./../components/MyTitle.vue";
import MyHeader from "./../components/MyHeader.vue";
import MyText from "./../components/MyText.vue";
import MyInfoCard from "./../components/MyInfoCard.vue";
export default {
  components: {
    MyButton,
    MyTitle,
    MyHeader,
    MyText,
    MyInfoCard,
  },
};
</script>

<template>
  <main>
    <MyTitle />
    <MyTitle size="big" label="grand titre h1" />
    <MyTitle size="tiny" type="h2" label="petit titre h2" />
    <MyButton label="Cliquez ici" href="/lien" />

    <MyHeader />
    <MyTitle size="-little" label="test" />
    <MyText size="-body" label="blabla" />
    <MyText size="-liens" label="blabla" />
    <MyInfoCard />
  </main>
</template>
