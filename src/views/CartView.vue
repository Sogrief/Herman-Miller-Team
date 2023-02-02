<template>

    <MyHeader />

    
    <div class="panier">
        <div class="panier__item" v-for="addedProducts in $store.state.products">
            <div class="panier__item__product">
                <div class="panier__item__product__img">                
                    <img v-bind:src="addedProducts.images[0].src">
                    <div>
                        <MyButton class="button-quantite" label="-" @click="removeFromCart(addedProducts)"/>
                        {{addedProducts.quantity}}
                        <MyButton class="button-quantite" label="+" @click="addToCart(addedProducts)"/>
                    </div>
                </div>
            </div>

            <div class="panier__item__infos">
                <div>{{addedProducts.name}}</div>
                <div>prix total : {{ addedProducts.quantity*addedProducts.price }} €</div>
            </div>

            <div class="panier__item__sideButtons">
                <RouterLink :to="`/products/${addedProducts.slug}`" target="_blank">
                    <MyButton class="button" label="personnaliser" />
                </RouterLink>

                <img src="/assets/icones/trash.svg" @click="deleted(addedProducts)">
            </div>
        </div>
    </div>

</template>

<script>
import MyHeader from "@/components/MyHeader.vue";
import MyButton from "@/components/MyButton.vue";

export default {
    components: { 
    MyHeader, 
    MyButton
    },

    methods:{
        addToCart(addedProducts){
            this.$store.commit("add", addedProducts);
            console.log(addedProducts.quantity);
        },

        removeFromCart(addedProducts){
            if (addedProducts.quantity==1){
                addedProducts.quantity=0;
                this.$store.commit("remove", addedProducts.id);
            }

            else{
                addedProducts.quantity--;
            }
        },

        deleted(deleteProduct){
            this.$store.commit("remove", deleteProduct.id);
        },
    }
}

</script>
  
<style lang="scss">

.panier{
    display:flex;
    flex-wrap:wrap;
    flex-direction:column;
    width:50vw;
    row-gap:pxToRem(30);

    &__item{
        border:1px solid #01E6B6;
        display: flex;
        align-items: center;
        padding:pxToRem(15);

        &__product{
            &__img{
                display: flex;
                flex-direction: column;
                align-items:center;
                width:pxToRem(200);
                @include bodyText();
                filter: drop-shadow(0px 0px 25px rgb(67, 67, 67));
                row-gap: pxToRem(20);

                img{
                    width:10vw;
                }
            }
        }
        
        &__infos{
            display: flex;
            flex-direction: column;
            row-gap: pxToRem(7);
            @include bodyText();
        }

        &__sideButtons{
            display: flex;
            flex-grow: 1;
            align-self: flex-start;
            justify-content:flex-end;
            column-gap: pxToRem(20);

            img{
                width:pxToRem(20);
            }
        }
    }
}

</style>
  