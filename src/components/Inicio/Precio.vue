<template>
  <div>
    <v-card elevation="4" style="padding-top: 2rem">
      <v-row>
        <v-col cols="12" xs="1" sm="1" md="1" lg="1"></v-col>

        <v-col
          cols="12"
          md="2"
          class="d-none d-sm-none d-md-flex d-lg-flex d-xl-flex"
        >
          <v-text-field
            type="number"
            min="0"
            color="amber"
            label="Precio:"
            placeholder="Min..."
            outlined
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"
          lg="2"
          md="2"
          class="d-none d-sm-none d-md-flex d-lg-flex d-xl-flex"
        >
          <v-text-field
            type="number"
            min="0"
            color="amber"
            label="Hasta:"
            placeholder="Max.."
            outlined
          ></v-text-field>
        </v-col>
        <v-col
          cols="9"
          xs="1"
          lg="3"
          md="3"
          sm="4"
          style="padding-left: 1.5rem"
        >
        <!--REVISAR POR QUE NO MUESTRA LOS CHECKBOX EN EL DRAWER-->
          <v-select
            :items="items"
            label="Ordenar por:"
            v-model="opcion"
            outlined
            prepend-inner-icon="mdi-view-headline"
          ></v-select>
        </v-col>
        <v-col
          cols="2"
          xs="1"
          sm="4"
          class="d-sm-flex d-md-none d-lg-none d-xl-none"
        >
          <v-btn
            fab
            dark
            color="amber"
            icon
            elevation="1"
            @click.stop="drawer = !drawer"
          >
            <v-icon color="amber"> mdi-filter </v-icon>
          </v-btn>
        </v-col>
        <v-col
          cols="12"
          md="2"
          lg="1"
          class="d-none d-sm-none d-md-flex d-lg-flex d-xl-flex"
        >
          <v-btn
            color="orange"
            block
            x-large
            elevation="2"
            outlined
            margin="auto"
          >
            <v-icon> mdi-magnify </v-icon>
            Buscar</v-btn
          >
        </v-col>
      </v-row>
      <v-navigation-drawer
        v-model="drawer"
        app
        absolute
        temporary
        max-height="100"
        color="blue-grey lighten-5"
        style="margin-left: -1rem; padding-top: -2rem"
      >
        <!--Codigo del Filtrado debe ir aqui-->
        <v-card elevation="3" class="d-none d-lg-flex d-xl-flex d-md-flex">
          <v-container
            style="
              padding-left: 1.4rem;
              margin-bottom: 1rem;
              padding-right: 5rem;
            "
          >
            <h2 class="amber--text text-center" style="padding-top: 1rem">
              Filtrar por:
            </h2>

            <v-switch
              color="amber"
              style="font-weight: bold"
              inset
              label="Nuevo"
            ></v-switch>
            <br />
            <v-divider></v-divider>
            <h3 class="amber--text">Marca</h3>
            <div>
              <v-checkbox
                style="margin-bottom: -1.5rem"
                color="amber darken-4"
                v-model="marcas"
                value="iPhone"
                :label="`iPhone`"
                @click="filtrarProductos()"
              >
              </v-checkbox>
              <v-checkbox
                style="margin-bottom: -1.5rem"
                color="amber darken-4"
                v-model="marcas"
                value="Samsung"
                :label="`Samsung`"
                @click="filtrarProductos()"
              >
              </v-checkbox>
              <v-checkbox
                style="margin-bottom: -1.5rem"
                color="amber darken-4"
                v-model="marcas"
                value="Realme"
                :label="`Realme`"
                @click="filtrarProductos()"
              >
              </v-checkbox>
              <v-checkbox
                style="margin-bottom: -1.5rem"
                color="amber darken-4"
                v-model="marcas"
                value="Huawei"
                :label="`Huawei`"
                @click="filtrarProductos()"
              >
              </v-checkbox>
              <v-checkbox
                style="margin-bottom: -1.5rem"
                color="amber darken-4"
                v-model="marcas"
                value="Xiaomi"
                :label="`Xiaomi`"
                @click="filtrarProductos()"
              >
              </v-checkbox>
            </div>

            <br />
            <v-divider></v-divider>
            <h3 class="amber--text">Sistema</h3>
            <v-checkbox
              style="margin-bottom: -1.5rem"
              color="amber darken-4"
              v-model="sistemas"
              value="iOS"
              :label="`iOS`"
              @click="filtrarProductos()"
            >
            </v-checkbox>
            <v-checkbox
              style="margin-bottom: -1.5rem"
              color="amber darken-4"
              v-model="sistemas"
              value="Android"
              :label="`Android`"
              @click="filtrarProductos()"
            >
            </v-checkbox>
            <br />
            <v-divider></v-divider>
            <h3 class="amber--text">Pantalla</h3>
            <v-checkbox
              style="margin-bottom: -1.5rem"
              color="amber darken-4"
              v-model="pantallas"
              value="5"
              :label="`5''`"
              @click="filtrarProductos()"
            >
            </v-checkbox>
            <v-checkbox
              style="margin-bottom: -1.5rem"
              color="amber darken-4"
              v-model="pantallas"
              value="6"
              :label="`6''`"
              @click="filtrarProductos()"
            >
            </v-checkbox>
            <v-checkbox
              style="margin-bottom: -1.5rem"
              color="amber darken-4"
              v-model="pantallas"
              value="7"
              :label="`7''`"
              @click="filtrarProductos()"
            >
            </v-checkbox>
          </v-container>
        </v-card>
      </v-navigation-drawer>
    </v-card>
  </div>
</template>


<script>
import { db } from "./../../db";
import { bus } from "./../../main";
export default {
  name: "Precio",
  data() {
    return {
      drawer: false,
      marcas: [],
      sistemas: [],
      pantallas: [],
      switch1: false,
      productos: [],
      range: [0, 1000],
      opcion: [
        "iPhone",
        "Samsung",
        "Huawei",
        "OnePlus",
        "Xiaomi",
        "Realme",
      ],
      checksistemas: ["iOS", "Android"],
      tamanios: ['5"', '5,5"', '6"', '7"', '8"'],
    };
  },

  methods: {
    llenarArray() {
      db.collection("celulares")
        .get()
        .then((data) => {
          data.forEach((element) => {
            this.productos.push(element.data());
            console.log(element.data());
          });
        });
      console.log("el tamanio: " + this.productos.length);

      this.filtrarProductos();
    },

    filtrarProductos() {
      bus.$emit("FProductos", this.selectedItems());
      console.log(this.marcas);
      console.log(this.selectedItems().length);
    },

    selectedItems() {
      if (this.productos.length == 0) {
        return this.productos;
      } else {
        return this.productos.filter(function (newProductos) {
          console.log("opcion 0");
          if (
            this.marcas.length > 0 ||
            this.pantallas.length > 0 ||
            this.sistemas.length > 0
          ) {
            if ((this.marcas.length > 0) & (this.pantallas.length > 0)) {
              console.log("opcion 1");
              return (
                this.marcas.includes(newProductos.marca) &
                this.pantallas.includes(newProductos.pantalla)
              );
            } else if ((this.marcas.length > 0) & (this.sistemas.length > 0)) {
              console.log("opcion 2");
              return (
                this.marcas.includes(newProductos.marca) &
                this.sistemas.includes(newProductos.sistema)
              );
            } else if (
              (this.sistemas.length > 0) &
              (this.pantallas.length > 0)
            ) {
              console.log("opcion 3");
              return (
                this.sistemas.includes(newProductos.sistema) &
                this.pantallas.includes(newProductos.pantalla)
              );
            } else {
              console.log("opcion 4");
              return (
                this.marcas.includes(newProductos.marca) ||
                this.sistemas.includes(newProductos.sistema) ||
                this.pantallas.includes(newProductos.pantalla)
              );
            }
          } else {
            console.log("opcion 5");
            return (
              !this.marcas.includes(newProductos.marca) &
              !this.sistemas.includes(newProductos.sistema) &
              !this.pantallas.includes(newProductos.pantalla)
            );
          }
        }, this);
      }
    },
  },

  firestore: {
    productos: db.collection("celulares"),
  },

  mounted() {
    this.filtrarProductos();
  },
  watch: {
    group() {
      this.drawer = false;
    },
  },
};
</script>

<style lang="scss" scoped></style>
