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
          label:
            "Vous avez de la chance : la livraison est gratuite ! Comptez un délai de 7 à 15 jours en fonction du pays de destination",
        },
        {
          id: 2,
          title: "Retours faciles",
          srcImage: "../../assets/icones/boîte.svg",
          label:
            "Vous n’êtes pas satisfait(e) ? Il vous suffit de retourner votre produit. Les retours effectués dans un délai de 14 jours seront toujours acceptés.",
        },
        {
          id: 3,
          title: "Garantie unique sur le marché",
          srcImage: "../../assets/icones/check.svg",
          label:
            "Nos produits sont conçus pour durer, et la plupart d’entre eux sont couverts par une garantie de 12 ans.",
        },
      ],
    };
  }
};
</script>

<template>
  <div class="bg-perspective">
    <div class="list grid">
      <MyInfo
        v-for="information in informations"
        :key="information.id"
        :class="title - big"
        :title="information.title"
        :srcImage="information.srcImage"
        :label="information.label"
      />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.list {
  height: 600px;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.bg-perspective {
  background-size: cover;
  background-image: url(../../assets/images/perspective_grille.svg);
}
</style>
