<script>
import MyButton from "./../components/MyButton.vue";
import MyTitle from "./../components/MyTitle.vue";
import MyHeader from "./../components/MyHeader.vue";
export default {
  components: {
    MyButton,
    MyTitle,
    MyHeader,
  },
};
</script>

<template>
  <main>
    <MyHeader />
    <MyTitle />
    <MyTitle size="big" label="grand titre h1" />
    <MyTitle size="tiny" type="h2" label="petit titre h2" />
    <MyButton label="Cliquez ici" href="/lien" />
    <MyButton label="Validez le formulaire" type="secundary" />
  </main>
</template>
