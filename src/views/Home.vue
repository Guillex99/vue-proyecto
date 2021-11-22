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
    <v-row style="padding-top: 2rem">
      <v-col cols="12">
        <v-footer padless>
          <v-col class="text-center" cols="12">
            {{ new Date().getFullYear() }} — <strong>Guillermo Enrique Martinez Figueroa MF17006</strong>
          </v-col>
        </v-footer>
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
