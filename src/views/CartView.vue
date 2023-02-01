<template>

    <MyHeader />


    {{ $store.state.products.name}}

    <div class="panier" v-for="addedProducts in $store.state.products">
        <div>
            <div>{{addedProducts.name}}</div>
            <div>{{addedProducts.price}}</div>
            <div>{{addedProducts.quantity}}</div>
            <img v-bind:src="addedProducts.images[0].src">
        </div>
    </div>

</template>

<script>
import MyHeader from "@/components/MyHeader.vue";

export default {
    components: { 
    MyHeader, 
    },
}

</script>
  
<style lang="scss">

</style>
  