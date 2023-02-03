<script>
export default {
data() {
return {
  showModal: false,
};
},

methods: {
openModal() {
  this.showModal = true;
},
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
      top: 180px;
      left: 250px;
    }
}
}

.modal-background {
  position: absolute;
  bottom: 40px;
  left: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  padding: 20px;
  border: 1px $mainColor solid;
}
</style>