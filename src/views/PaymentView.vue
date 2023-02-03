<template>

<DefaultLayout>
        <template v-slot:header>
          <MyHeader />
        </template>

    <div class="order-view">
    <div class="container">
      <h1 class="order-view__title">Commander</h1>
      <form action="" class="order-view__form">
        <h2 class="order-view__subtitle">Informations de facturation</h2>
        <div class="order-view__row || row">
          <div class="column -size-6">
            <div class="order-view__field">
                <MyInput label="Prénom" type="text" v-model="form.billing.first_name" />
            </div>
          </div>
          <div class="column -size-6">
            <div class="order-view__field">
                <MyInput label="Nom" type="text" v-model="form.billing.last_name" />
            </div>
          </div>
        </div>
        <div class="order-view__row || row">
          <div class="column -size-6">
            <div class="order-view__field">
                <MyInput label="Adresse" type="text" v-model="form.billing.address_1" />
            </div>
          </div>
          <div class="column -size-6">
            <div class="order-view__field">
                <MyInput label="Complément d'adresse" type="text" v-model="form.billing.address_2" />
            </div>
          </div>
        </div>
        <div class="order-view__row || row">
          <div class="column -size-6">
            <div class="order-view__field">
              <MyInput label="Ville" type="text" v-model="form.billing.city" />
            </div>
          </div>
          <div class="column -size-6">
            <div class="order-view__field">
                <MyInput label="Etat/région" type="text" v-model="form.billing.state" />
            </div>
          </div>
        </div>
        <div class="order-view__row || row">
          <div class="column -size-6">
            <div class="order-view__field">
                <MyInput label="Code postal" type="text" v-model="form.billing.postcode" />
            </div>
          </div>
        </div>
        <div class="order-view__row || row">
          <div class="column -size-6">
            <div class="order-view__field">
                <MyInput label="Email" type="email" v-model="form.billing.email" />
            </div>
          </div>
          <div class="column -size-6">
            <div class="order-view__field">
             <MyInput label="Téléphone" type="email" v-model="form.billing.phone" />
            </div>
          </div>
        </div>
        <div class="order-view__row || row">
          <div class="column -size-12">
            <input id="billing-shipping" type="checkbox" v-model="otherAddress">
            <label for="billing-shipping">Je souhaite livrer à une autre adresse</label>
          </div>
        </div>
        <div v-if="otherAddress" class="order-view__shipping">
          <h2 class="order-view__subtitle">Informations de livraison</h2>
          <div class="order-view__row || row">
            <div class="column -size-6">
              <div class="order-view__field">
                <MyInput label="Prénom" type="text" v-model="form.shipping.first_name"/>
              </div>
            </div>
            <div class="column -size-6">
              <div class="order-view__field">
                <MyInput label="Nom" type="text" v-model="form.shipping.last_name"/>
                </div>
            </div>
          </div>
          <div class="order-view__row || row">
            <div class="column -size-6">
              <div class="order-view__field">
                <MyInput label="Adresse" type="text" v-model="form.shipping.address_1" />
               </div>
            </div>
            <div class="column -size-6">
              <div class="order-view__field">
                <MyInput label="Complément d'adresse" type="text" v-model="form.shipping.address_2" />
              </div>
            </div>
          </div>
          <div class="order-view__row || row">
            <div class="column -size-6">
              <div class="order-view__field">
                <MyInput label="Ville" type="text" v-model="form.shipping.city" />
              </div>
            </div>
            <div class="column -size-6">
              <div class="order-view__field">
                <MyInput label="Etat/région" type="text" v-model="form.shipping.state" />
              </div>
            </div>
          </div>
          <div class="order-view__row || row">
            <div class="column -size-6">
              <div class="order-view__field">
                <MyInput label="Code postal" type="text" v-model="form.shipping.postcode" />
              </div>
            </div>
          </div>
        </div>
        <Loader v-if="loading" />
        <div v-else class="order-view__submit">
            <MyButton :label="'Valider la commande'" @click="confirmOrder"/>
        </div>
      </form>
      <div v-if="message.text" :class="['order-view__message', `-is-type-${message.type}`]">
        {{ message.text }}
      </div>
    </div>
  </div>

  <template v-slot:footer>
          <MyFooter />
        </template>
      </DefaultLayout>
</template>

<script>
import {client} from "@/outils/axios"
import MyHeader from "@/components/MyHeader.vue";
import MyFooter from "@/components/MyFooter.vue";
import MyButton from "@/components/MyButton.vue"
import MyInput from "@/components/MyInput.vue";
import MyTitle from "../components/MyTitle.vue";
import DefaultLayout from "@/layout/DefaultLayout.vue";

export default {
    components: { 
    MyHeader, 
    MyInput,
    MyButton,
    MyTitle,
    MyFooter,
    DefaultLayout,
    },
    data () {
    return {
      form: {
        billing: {
          first_name: '',
          last_name: '',
          address_1: '',
          address_2: '',
          city: '',
          state: '',
          postcode: '',
          country: '',
          email: '',
          phone: ''
        },
        shipping: {
          first_name: '',
          last_name: '',
          address_1: '',
          address_2: '',
          city: '',
          state: '',
          postcode: '',
          country: ''
        },
      },
      loading: false,
      otherAddress: false,
      message: {}
    }
  },

  methods: {
    async confirmOrder () {
      this.loading = true
      // Create array from store product array with only needed keys
      const lineItems = this.$store.state.products.map((product) => {
        return {
          product_id: product.id,
          quantity: product.quantity
        }
      })

      try {
        // Trigger a POST request on the order endpoint to create an order
        const response = await client.post(`${import.meta.env.VITE_WP_API_URL}/wc/v3/orders`, {
          payment_method: "paypal",
          payment_method_title: "PayPal",
          set_paid: true,
          billing: this.form.billing,
          shipping: this.otherAddress ? this.form.shipping : this.form.billing,
          line_items: lineItems
        })

        this.loading = false

        // Request has succeeded. Display a success message
        this.message = { type: 'success', text: 'Votre commande a bien été enregistrée' }
        this.$store.commit('emptyCart')
        this.form = {
          billing: {
            first_name: '',
            last_name: '',
            address_1: '',
            address_2: '',
            city: '',
            state: '',
            postcode: '',
            country: '',
            email: '',
            phone: ''
          },
          shipping: {
            first_name: '',
            last_name: '',
            address_1: '',
            address_2: '',
            city: '',
            state: '',
            postcode: '',
            country: ''
          }
        }


      } catch (err) {
        // Request has failed. Display an error message
        this.loading = false
        this.message = { type: 'error', text: 'Une erreur est survenue' }
      }
    }
  }
}

</script>
  
<style lang="scss">
label {
  @include bodyText();
}
    .order-view {
  padding: 50px;

  &__form {
    margin-top: 50px;
  }

  &__row {
    margin-top: 20px;
  }

  &__field {
    display: flex;
    flex-flow: column wrap;
  }

  &__label {
    font-size: 16px;
    font-weight: 700;
  }

  &__input {
    padding: 10px;
    font-size: 16px;
  }

  &__submit {
    margin-top: 30px;
  }

  &__message {
    font-size: 16px;
    font-weight: 700;
    color: red;
    text-align: center;
    margin-top: 20px;

    &.-is-type-success {
      color: darkslategrey;
    }
    input[type="checkbox"]{
        display: none;
        + label {
            width: 15px;
            height: 15px;
            border: 1px solid $bodyText;
            cursor: pointer;
            display: inline-block;
        }
    }
  }

}
</style> 