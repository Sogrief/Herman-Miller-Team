<template>

    <MyHeader />
    <div class="container">
        <div class="panier">
            <div class="panier__item" v-for="addedProducts in $store.state.products">
                <div class="panier__item__product">
                    <div class="panier__item__product__img">   
                        <!--<div v-if="addedProducts.images[0].src">
                            <img v-bind:src="addedProducts.images[0].src">
                        </div>     -->        
                        {{  addedProducts}}
                        
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
                    <RouterLink :to="`/boutique/${addedProducts.slug}`" target="_blank">
                        <MyButton class="button" label="personnaliser" />
                    </RouterLink>

                    <img src="/assets/icones/trash.svg" @click="deleted(addedProducts)">
                </div>
            </div>
        </div>

        <div class="panneauReduc">
            <div class="panneauReduc__reduc">
                <div class="panneauReduc__reduc__input">
                    <label>réduction</label>
                    <input type="text"/>
                </div>
                <MyButton class="button" label="appliquer" />
            </div>

            <div class="panneauReduc__total">total {{ total }}€</div>
            <div class="panneauReduc__infos">
                <div><img src="/assets/images/casesBiseaux.svg"> Retours gratuits</div>
                <div><img src="/assets/images/casesBiseaux.svg"> 12 ans de garantie</div>
                <div><img src="/assets/images/casesBiseaux.svg"> Livraison rapide</div>
            </div>
            <div class="panneauReduc__paiement">
                <MyButton class="button -suivant" label="procéder au paiement " />
                <RouterLink :to="`/products`">
                    <MyButton class="button -precedent" label="continuer mes achats" />
                </RouterLink>
            </div>
        </div>
    </div>

</template>

<script>
import MyHeader from "@/components/MyHeader.vue";
import MyButton from "@/components/MyButton.vue";
import MyInput from "@/components/MyInput.vue";

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
    },

    computed: {
            total () {
            return this.$store.state.products.reduce((total, addedProducts) => {
                return total + (addedProducts.quantity * addedProducts.price)
            }, 0)
        }
    }
}

</script>
  
<style lang="scss">

.container{
    display: flex;
    flex-wrap: wrap;
    row-gap: pxToRem(60);
    column-gap:3vw;
    justify-content: center;
    align-items: flex-start;
}

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

.panneauReduc{
    width:40vw;
    background-image: url(/assets/images/encartsBiseauxEpais.png);
    background-size: 100% 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    row-gap: pxToRem(30);
    padding: pxToRem(100);

    &__reduc{
        display: flex;
        align-items: flex-end;
        column-gap:2vw;

        &__input{
            label
            {
                @include title;
            }

            input
            {
                display:block;
                border:1px solid $bodyText;
                padding:pxToRem(5);
                background-color: $backgroundColor;
            }
        }
    }

    &__total{
        @include title;
    }

    &__infos{
        @include bodyText;
    }

    &__paiement{
        display: flex;
        flex-wrap: wrap;
        flex-direction: column;
        row-gap: pxToRem(10);
    }
}

@media screen and (max-width: map-get($breakpoints, "tablet-down")) {
    .container{
        flex-direction: column;
    }
}

</style>
  