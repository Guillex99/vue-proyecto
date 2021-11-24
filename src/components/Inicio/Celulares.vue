<template>
  <div>
    <v-row>
      <v-col
        v-for="(celular, key) in telefonos"
        :key="key"
        cols="6"
        md="4"
        lg="4"
        xl="4"
        style="padding-top: 2rem"
      >
        <!--INICIO DE MI CARD-->
        <v-card
          class="mx-auto"
          max-width="344"
          elevation="4"
          height="450px"
          min-height="400px"
          max-height="600px"
        >
          <v-img
            class="black--text align-end"
            :aspect-ratio="16 / 9"
            height="200px"
            :src="celular.imagenes[0]"
          >
          </v-img>
          <v-card-title
            style="color: green; font-weight: bold; justify-content: center"
          >
            ${{ celular.precio }}
          </v-card-title>
          <v-card-subtitle
            style="
              font-weight: 500;
              justify-content: justify;
              padding-bottom: 2rem;
              height: 100px;
            "
          >
            {{ celular.titulo }}
          </v-card-subtitle>
          <div class="text-center" style="padding-bottom: 1rem">
            <v-btn rounded color="amber" dark :to="'/detalle/' + celular.id">
              <!--Ver detalle-->
              Ver detalle
            </v-btn>

            <v-btn rounded color="orange" dark
            @click="agregar(celular)"
            
            >
              <!--Ver detalle-->
              <v-icon>mdi-cart</v-icon>
            </v-btn>
          </div>
        </v-card>

        <!--FIN DE MI CARD-->
      </v-col>
    </v-row>
  </div>
</template>

<script>
// import { db } from "./../../db";
import { bus } from "./../../main";

export default {
  name: "Celulares",
  data() {
    return {
      telefonos: [],
    };
  }, 
  methods: {
    agregar(anuncio){
      //this.anuncio.imagen = anuncio.imagenes[0];
      this.$emit('addCart', anuncio);
    }
  },
   /* firestore: {
     telefonos: db.collection("celulares"),
   }, */

  created() {
    bus.$on("FProductos", (data) => {
      this.telefonos = data;
    });
  },
};
</script>

<style lang="scss" scoped></style>
