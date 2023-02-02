<script>
import { client } from "@/outils/axios";
import MyText from "./../components/MyText.vue";
import { RouterLink } from 'vue-router';

export default {
  components: {
    RouterLink,
    MyText
  },
  data() {
    return {
      menuWP: [
        {
          label:'',
          link: '',
          icone: '',
        }
      ],
      logoURL: ''
    };
  },
  async mounted() {
        // Request Logo
        const logoResponse = await client.get(
      import.meta.env.VITE_WP_API_URL + "/wp/v2/settings"
    );
    const logoID = logoResponse.data.site_logo;
    const mediaResponse = await client.get(
      import.meta.env.VITE_WP_API_URL + "/wp/v2/media/" + logoID
    );
    this.logoURL = mediaResponse.data.source_url;
    
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
        link: this.convertLinkToRoute(item.url),
        icone: item.thumbnail_src,
        // route: this.convertLinkToRoute(item.url),
      };
    });
  }
  this.menuWP.unshift({
    label: 'Logo',
    link: '',
    icone: this.logoURL,
  });
},
methods: {
  convertLinkToRoute(link) {
    if (!link) {
    return '';
  }
    const url = new URL(link);
  return url.pathname;
}},
}
</script>

<template>
  <div >
    <ul class="header__row">
      <li class="header -item" v-for="(item, index) in menuWP" :key="item.id">
        <template v-if="index === 0">
          <RouterLink class="header lien -menu" to="/">
            <img class="header-logo" :src="item.icone"/>
          </RouterLink>
        </template>
        <template v-else-if="item.icone">
          <RouterLink class="header lien -menu" :to=" item.link">
            <div>
              <img class="header-icone" :src="item.icone"/>
            </div>
          </RouterLink>
        </template>
        <template v-else>
          <RouterLink class="header lien -menu" :to=" item.link">{{ item.label }}</RouterLink>
        </template>
      </li>
    </ul>
  </div>
</template>





<style lang="scss">
.header {
  height: 56px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  &__row {
    padding: 20px;
    display: flex;
    flex-direction: row;
    list-style: none;
    justify-content: flex-end;
    align-items: center;
    gap: 20px;
  }
  &-icone {
    width: 22px;
  }
}

li.header:nth-child(1) {
 flex-grow: 1;
}


</style>
