<template>

    <MyHeader />

    {{ $store.state.products }}

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
  