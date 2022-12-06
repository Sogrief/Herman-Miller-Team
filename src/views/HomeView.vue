<script>
import MyButton from "./../components/MyButton.vue";
import MyTitle from "./../components/MyTitle.vue";
import MyHeader from "./../components/MyHeader.vue";
import MyText from "./../components/MyText.vue";
import MyInfoCard from "./../components/MyInfoCard.vue";
import MyCheckbox from "./../components/MyCheckbox.vue";
import MyInput from "./../components/MyInput.vue";
import MyCatalogItem from "../components/MyCatalogItem.vue";
import MyCatalogList from "../components/MyCatalogList.vue";

export default {
  components: {
    MyButton,
    MyTitle,
    MyInput,
    MyHeader,
    MyText,
    MyCatalogItem,
    MyInfoCard,
    MyCheckbox,
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

    <MyCatalogItem src="../../assets/images/produit 1.png" nomItem="embody" />
    <MyButton type="precedent" label="suivant" />
    <MyHeader />
    <MyCheckbox />
    <MyTitle size="-little" label="test" />
    <MyText size="-body" label="blabla" />
    <MyText size="-liens" label="blabla" />
    <MyInfoCard />

  </main>
</template>
