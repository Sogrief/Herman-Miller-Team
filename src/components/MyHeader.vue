<script>
import { client } from "@/outils/axios";
import MyText from "./../components/MyText.vue";
import { RouterLink } from 'vue-router';
export default {
  components: {
    RouterLink,
  },
  data() {
    return {
      menuWP: [
        {
          label:'',
          link: '',
          icone: ''
        }
      ],
    };
  },
//   async mounted() {
//     // Request Menu
//     const response = await client.get(
//       import.meta.env.VITE_WP_API_URL + "/wp/v2/menu-items"
//     );
//     this.response = response.data;
//     this.menuWP = this.response.items.map((item) => {
//       let icone = '';
//       if (item['_links']['wp:featuredmedia']) {
//         icone = item['_links']['wp:featuredmedia'][0].href;
//       }
//       return {
//         id: item.id,
//         label: item.title,
//         link: item.url,
//         icone: icone,
//       }  
//     })
//   }
// }
async mounted() {
    // Request Menu
    const response = await client.get(
      import.meta.env.VITE_WP_API_URL + "/menus/v1/menus/principal"
    );
    this.response = response.data;
    if (this.response && this.response.items) {
      this.menuWP = this.response.items.map((item) => {
        return {
          id: item.id,
          label: item.title,
          link: item.url,
          icone: item.thumbnail_src,
        };
      });
    }
    console.log(this.menuWP)
  }
}

</script>

<!-- Pour afficher les éléments du menu : wp/v2/menu-items -->

<template>
  
  <!--
Ce code la fonctionne avec le plugin Menu image. Le problème c'est qu'il récupère bien l'url du svg, mais n'arrive pas à montrer vraiment l'icone. 


const response = await client.get(
  import.meta.env.VITE_WP_API_URL + "/menus/v1/menus/principal"
);
this.response = response.data;
this.menuWP = this.response.items.map((item) => {
  return {
    id: item.id,
    label: item.title,
    link: item.url,
    icone: item.thumbnail_src,
  }  
})
}
}
-->
<div class="header">
    <ul>
      <li v-for="item in menuWP" :key="item.id">
        <a v-if="item.icone" :href="item.link">
          <img :src="item.icone" />
        </a>
        <a v-else :href="item.link">{{ item.label }}</a>
      </li>
    </ul>
  </div>


<!-- Avec le plugin menu icon de themselse, on peut récupérer une image via cette autre requete https://projet-herman.online/wp-json/wp/v2/menu-items/90
Le problème, c'est que l'image se situe dans "href" est dans l'attribut ""wp:featuredmedia" qui est lui même dans "_links" -->


</template>

<style lang="scss">
.header {
  height: 56px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  &__row {
    display: flex;
    flex-direction: row;
    list-style: none;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
  }
  &-svg {
    width: 20px;
  }
}
</style>
