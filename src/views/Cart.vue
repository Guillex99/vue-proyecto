<template>
  <div>
    <NavbarGrande v-bind:carrito="this.$route.params.carrito"></NavbarGrande>
    <br />
    <h1 class="text-center amber--text">Carrito</h1>
    <br />
    <v-container>
      <v-card
        elevation="6"
        style="padding-top: 1rem; margin-bottom: 2rem; padding-bottom: 1rem"
        v-for="(anuncio, id) in $route.params.carrito"
        :key="id"
      >
        <v-row>
          <v-col cols="5" xs="3" sm="3" md="3" lg="3" xl="3">
            <v-img
              :src="anuncio.producto.imagenes[0]"
              max-height="400px"
              max-width="75%"
            >
            </v-img>
          </v-col>
          <v-col cols="5" xs="3" sm="3" md="5" lg="5" xl="5">
            <h3>
              <span style="font-weight: 500; color: orange"
                >{{ anuncio.producto.marca }}
                {{ anuncio.producto.modelo }}</span
              >
            </h3>
            <h3 style="color: green">${{ anuncio.producto.precio }}</h3>
            <h4>
              Vendedor:
              <span style="font-weight: 300">{{
                anuncio.producto.vendedor
              }}</span>
            </h4>
            <h4>
              Estado:
              <span style="font-weight: 300">{{
                anuncio.producto.estado
              }}</span>
            </h4>
            <h4>
              ROM:
              <span style="font-weight: 300">{{ anuncio.producto.rom }}GB</span>
            </h4>
            <h4>
              RAM:
              <span style="font-weight: 300">{{ anuncio.producto.ram }}GB</span>
            </h4>
          </v-col>
          <v-col cols="4" md="4" lg="4" xl="4">
            <div class="mx-auto">
              <v-btn             
                @click="menos(id)"
                v-if="anuncio.cantidad == 1"
                style="background-color:red;"
              >
                <v-icon color="white">mdi-delete</v-icon>
              </v-btn>

              <v-btn style="" @click="menos(id)" v-if="anuncio.cantidad > 1"
                ><v-icon>mdi-minus</v-icon>
              </v-btn>
              <div class="d-inline col-1">
                {{ anuncio.cantidad }}
              </div>
              <v-btn style="" @click="mas(id)">
                <v-icon>mdi-plus</v-icon>
              </v-btn>
            </div>
          </v-col>
        </v-row>
      </v-card>
    </v-container>
  </div>
</template>

<script>
import { db } from "./../db";
import NavbarGrande from "./../components/navbars/NavbarGrande.vue";
export default {
  name: "Cart",
  components: {
    NavbarGrande,
  },
  data() {
    return {
      carrito: [],
      
    };
  },
  methods: {
    menos(id){
      if(this.$route.params.carrito[id].cantidad == 1){
        this.$route.params.carrito.splice(id, 1)
      }else{
        this.$route.params.carrito[id].cantidad = this.$route.params.carrito[id].cantidad - 1 
        this.$route.params.carrito[id].subtotal = this.$route.params.carrito[id].cantidad * this.$route.params.carrito[id].producto.precio
      }
    },

    mas(id){
      this.$route.params.carrito[id].cantidad = this.$route.params.carrito[id].cantidad + 1
      this.$route.params.carrito[id].subtotal = this.$route.params.carrito[id].cantidad * this.$route.params.carrito[id].producto.precio
    },
    },

  firestore: {
    carrito: db.collection("celulares"),
  },
  mounted() {
    console.log(this.$route.params.carrito);
    // if (this.$route.params.carrito != undefined) {

    //}
  },
};
</script>

<style lang="scss" scoped>
</style>