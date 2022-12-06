<script>
import MyInfo from "./MyInfo.vue";
export default {
  components: {
    MyInfo,
  },
  data() {
    return {
      informations: [
        {
          id: 1,
          title: "Livraison Gratuite",
          srcImage: "../../assets/icones/truck.svg",
          content:
            "Vous avez de la chance : la livraison est gratuite ! Comptez un délai de 7 à 15 jours en fonction du pays de destination",
        },
        {
          id: 2,
          title: "Retours faciles",
          srcImage: "../../assets/icones/boîte.svg",
          content:
            "Vous n’êtes pas satisfait(e) ? Il vous suffit de retourner votre produit. Les retours effectués dans un délai de 14 jours seront toujours acceptés.",
        },
        {
          id: 3,
          title: "Garantie unique sur le marché",
          srcImage: "../../assets/icones/check.svg",
          content:
            "Nos produits sont conçus pour durer, et la plupart d’entre eux sont couverts par une garantie de 12 ans.",
        },
      ],
    };
  },
};
</script>

<template>
  <div class="list">
    <MyInfo
      v-for="information in informations"
      :key="information.id"
      :title="information.title"
      :srcImage="information.srcImage"
      :content="information.content"
    />
  </div>
</template>

<style lang="scss" scoped>
.list {
  display: flex;
}
</style>
