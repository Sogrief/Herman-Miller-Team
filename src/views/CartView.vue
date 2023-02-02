<template>

    <MyHeader />


    {{ $store.state.products[0]}}
    <div>
        
    </div>
    <div class="panier">
        <div class="panier__item" v-for="addedProducts in $store.state.products">
            <div class="panier__item__product">
                <div class="panier__item__product__img">                
                    <img v-bind:src="addedProducts.images[0].src">
                    <div>
                        <MyButton class="button-quantite" label="-" />
                        <MyButton class="button-quantite" label="+" />
                    </div>
                </div>
            </div>

            <div class="panier__item__infos">
                <div>{{addedProducts.name}}</div>
                <div>{{addedProducts.price}}€</div>
                <div>{{addedProducts.quantity}}</div>
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
}

</script>
  
<style lang="scss">

.panier{
    display:flex;
    flex-wrap:wrap;
    flex-direction:column;
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
                filter: drop-shadow(0px 0px 25px rgb(67, 67, 67));

                img{
                    width:100%;
                }
            }
        }
        
        &__infos{
            display: flex;
            flex-direction: column;
            row-gap: pxToRem(7);
            @include bodyText();
        }
    }
}

</style>
  