<template>
 <v-row>
    <v-col cols="3">
      <Filtrado></Filtrado>
    </v-col>
  </v-row>

 
</template>



<script>
import Filtrado from "./../components/Filtrado.vue";
export default {
  name: "Home",

  components: {
    Filtrado,
  },
};
</script>
