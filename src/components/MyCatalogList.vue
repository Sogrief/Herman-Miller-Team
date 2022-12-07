<script>

import MyCatalogItem from "../components/MyCatalogItem.vue";

export default{
    components:
    {
        MyCatalogItem,
    },

    data() {
    return {
      produits: [
        {
          id: 1,
          srcImage: "../../assets/images/chaiseEmbody.png",
          nomProduit: "Embody",
          prix:"1730€"
        },
        {
          id: 2,
          srcImage: "../../assets/images/chaiseAeron.png",
          nomProduit: "Aeron",
          prix:"1725€"
        },
        {
          id: 3,
          srcImage: "../../assets/images/chaiseVantum.png",
          nomProduit: "Vantum",
          prix:"1277€",
        },
        {
          id: 4,
          srcImage: "../../assets/images/chaiseSayl.png",
          nomProduit: "Embody",
          prix:"823€"
        },
        {
          id: 5,
          srcImage: "../../assets/images/supportEcran.png",
          nomProduit: "Support d'écran",
          prix:"316€"
        },
        {
          id: 6,
          srcImage: "../../assets/images/bureauNevi.png",
          nomProduit: "bureau nevi",
          prix:"2218.50€",
        },
        {
          id: 7,
          srcImage: "../../assets/images/lotEmbody.png",
          nomProduit: "lot embody",
          prix:"1471€",
        },
        {
          id: 8,
          srcImage: "../../assets/images/lotAeron.png",
          nomProduit: "lot aeron",
          prix:"2989.45€"
        },
        {
          id: 9,
          srcImage: "../../assets/images/lotSayl.png",
          nomProduit: "lot sayl",
          prix:"2985.20€"
        },
        {
          id: 10,
          srcImage: "../../assets/images/tubeNeonLed.png",
          nomProduit: "tube neon led",
          prix:"2218.50€",
        },
      ],
    };
  },
};
</script>

<template>

    <div class="catalog">
        <MyCatalogItem
            v-for="produit in produits"
            :key="produit.id"
            :srcImage="produit.srcImage"
            :nomProduit="produit.nomProduit"
            :prix="produit.prix"
        />
    </div>

</template>

<style lang="scss" scoped>

    .catalog
    {
        width:90vw;
        display:flex;
        flex-wrap: wrap;
        justify-content: space-around;//centre les produits à l'intérieur du catalogue
        margin:auto;
        row-gap: pxToRem(100);//espace chaque ligne de produits entre eux
    }

</style>