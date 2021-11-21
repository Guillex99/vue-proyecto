<template>
  <v-container>
    <v-row>
      <v-col
        cols="12"
        lg="3"
        sm="12"
        class="d-none d-md-none d-lg-flex d-xl-flex"
      >
        <Filtrado></Filtrado>
      </v-col>
      <v-col cols="12" lg="9" md="12" sm="6" xs="6" class="">
        <Precio></Precio>
        <Celulares></Celulares>
      </v-col>
      <v-col>
        <Paginacion></Paginacion>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Filtrado from "./../components/Filtrado.vue";
import Precio from "./../components/Inicio/Precio.vue";
import Celulares from "./../components/Inicio/Celulares.vue";
import Paginacion from "./../components/Inicio/Paginacion.vue";
export default {
  name: "Home",

  components: {
    Filtrado,
    Precio,
    Celulares,
    Paginacion,
  },
};
</script>
