<script>

export default{
    components:
    {
        catalogCard,
    },

    data() {
    return {
      produits: [
        {
          id: 1,
          srcImage: "../../assets/images/produit 1.png",
          nomItem: "Embody",
          prix:"1730€"
        },
        {
          id: 2,
          srcImage: "../../assets/images/produit 1.png",
          nomItem: "Aeron",
          prix:"1725€"
        },
        {
          id: 3,
          srcImage: "../../assets/images/produit 1.png",
          nomItem: "Vantum",
          prix:"1277€",
        },
      ],
    };
  },
};
</script>

<template>

    <div class="catalog">
        <catalogCard
            v-for="produit in produits"
            :key="produit.id"
            :srcImage="produit.srcImage"
            :nomItem="produit.nomItem"
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