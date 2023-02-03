<template>

<div class="points" @click="openModal">
  <span v-for="point in points" :key="point.id"></span>
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

<style>
.points {
position: absolute;
top: 0;
left: 0;
}
.points span {
width: 10px;
height: 10px;
background-color: red;
display: inline-block;
margin-right: 10px;
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