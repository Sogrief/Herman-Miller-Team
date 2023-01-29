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


<template>
  <div class="header">
    <ul>
      <li v-for="item in menuWP" :key="item.id">
        <a :href="item.link">
          <template v-if="item.icone">
          <img :src="item.icone" />
          </template>
          <template v-else> {{ item.label }}</template>
        </a>
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
