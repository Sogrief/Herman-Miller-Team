<script>
import MyButton from "./../components/MyButton.vue";
import MyTitle from "./../components/MyTitle.vue";
import MyHeader from "./../components/MyHeader.vue";
import MyText from "./../components/MyText.vue";
import MyInfoCard from "./../components/MyInfoCard.vue";
import MyCheckbox from "./../components/MyCheckbox.vue";
import MyInput from "./../components/MyInput.vue";
import MyCatalogList from "../components/MyCatalogList.vue";
import MyFooter from "./../components/MyFooter.vue";

export default {
  components: {
    MyButton,
    MyTitle,
    MyInput,
    MyHeader,
    MyText,
    MyInfoCard,
    MyCheckbox,
    MyCatalogList,
    MyFooter,
  },
};
</script>

<template>
  <main>
    <MyTitle />
    <MyTitle size="big" label="grand titre h1" />
    <MyTitle size="tiny" type="h2" label="petit titre h2" />
    <MyButton label="Cliquez ici" href="/lien" />
    <MyButton label="Validez le formulaire" type="secundary" />
    
    <form>
      <MyInput for="nom" label="oui oui french baguette, oui le croissant" type="text" />
    </form>

    <MyTitle size="-big" label="grand titre h1" />
    <MyTitle size="-default" type="h2" label="petit titre h2" />
    <MyButton type="precedent" label="suivant" />
    <MyButton type="quantite" label="+" />
    <MyButton type="precedent" label="+" />
    <MyButton type="suivant" label="+" />
    <MyButton label="+" />
    <MyHeader />
    <MyCheckbox />
    <MyTitle size="-little" label="test" />
    <MyText type="lien" label="blabla" size="body" />
    <MyInfoCard />
    <MyCatalogList />

    <MyFooter />
  </main>
</template>
