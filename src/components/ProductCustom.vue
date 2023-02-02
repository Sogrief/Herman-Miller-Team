<template>
<div class="custom">
  <div class="custom_points" @click="openModal">
    <img class="custom_points_img" src="../../assets/images/product_point.svg" v-for="point in points" :key="point.id">
  </div>
</div>


<modal v-if="showModal" @close="closeModal">
  <div class="variations">
    <div
      class="variation"
      v-for="variation in variations"
      :key="variation.id"
      @click="selectVariation(variation)"
    ></div>
  </div>
</modal>
</template>

<script>
export default {
data() {
return {
  showModal: false,
  points: [{ id: 1 }, { id: 2 }, { id: 3 }],
  selectedVariation: null
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

.variations {
display: flex;
background-color: pink;
flex-wrap: wrap;
}
.variation {
width: 50px;
height: 50px;
background-color: blue;
}
</style>