<template>
  <v-app id="inspire">
    <Navbars></Navbars>
    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
//import Filtrado from "./components/Filtrado.vue";
import Navbars from "./components/navbars/Navbars.vue";

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
