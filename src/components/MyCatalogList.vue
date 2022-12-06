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
          srcImage: "../../assets/images/produit 1.png",
          nomProduit: "Embody",
          prix:"1730€"
        },
        {
          id: 2,
          srcImage: "../../assets/images/produit 1.png",
          nomProduit: "Aeron",
          prix:"1725€"
        },
        {
          id: 3,
          srcImage: "../../assets/images/produit 1.png",
          nomProduit: "Vantum",
          prix:"1277€",
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
        display:flex;
    }

</style>