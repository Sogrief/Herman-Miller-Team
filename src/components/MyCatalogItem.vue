<script>

export default{
    props: 
    {
        src: String,
        nomItem:String,
    },
};
</script>

<template>

    <div class="catalog__item">
        <img :src="src" />
        <div class="catalog__item__name">{{nomItem}}</div>
    </div>

</template>

<style lang="scss" scoped>

    .catalog__item
    {
        display:flex;

        &__name
        {
            @include title;
        }
    }

</style>