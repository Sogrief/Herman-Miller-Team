<script>

export default{
    props: 
    {
        src: String,
    },
};
</script>

<template>

    <div class="catalog__item">
        <img :src="src" />
    </div>

</template>

<style>

</style>