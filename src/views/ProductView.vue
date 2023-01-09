<script>
import MyHeader from "@/components/MyHeader.vue";
import MyFooter from "@/components/MyFooter.vue";
import MyProductNav from "@/components/MyProductNav.vue";

export default {
  components: {
    MyProductNav,
    MyHeader,
    MyFooter,
  },
};
</script>

<template>
  <main>
    <MyHeader />
    <MyProductNav />
    <MyFooter />
  </main>
</template>
