<template>
<div class="custom">
  <div class="custom_points" @click="openModal">
    <img class="custom_points_img" src="../../assets/images/product_point.svg" v-for="point in points" :key="point.id">
  </div>
</div>

<div v-if="showModal" class="modal-background">
      <div class="modal-content">
        Contenu de la modale
      </div>
</div>

</template>

<script>
export default {
data() {
return {
  showModal: false,
  points: [{ id: 1 }, { id: 2 }, { id: 3 }],
};
},
props: {
product: {
  variations: [],
  type: Object,
  required: true,
}
},
methods: {
openModal() {
  this.showModal = true;
},
closeModal() {
  this.showModal = false;
},
selectVariation(variation) {
  this.selectedVariation = variation;
  this.closeModal();
}
}
};
</script>

<style lang="scss">
.custom{
  position: relative;
  &_points {
    position: relative;
    &_img{
      position: absolute;
      top: 300px;
      left: 50px;
    }
    &_img:nth-of-type(2){
      top: 100px;
      left: 220px;
    }
    &_img:nth-of-type(3){
      top:500px;
      left: 250px;
    }
}
}

.modal-background {
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
}
</style>