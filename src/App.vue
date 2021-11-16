<template>
  <v-app>
    <Navbars></Navbars>
    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
import Navbars from './components/navbars/Navbars.vue';
export default {
  name: "App",
  data: () => ({
    //
  }),
  components: {
    Navbars,
  },
};
</script>
