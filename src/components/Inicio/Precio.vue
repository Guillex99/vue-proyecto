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
        <v-card elevation="3" class="" style="">
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
                v-for="marca in marcas"
                :key="marca"
                :label="`${marca}`"
              >
              </v-checkbox>
            </div>

            <br />
            <v-divider></v-divider>
            <h3 class="amber--text">Sistema</h3>
            <v-checkbox
              style="margin-bottom: -1.5rem"
              color="amber darken-4"
              v-for="sistema in sistemas"
              :key="sistema"
              :label="`${sistema}`"
            >
            </v-checkbox>
            <br />
            <v-divider></v-divider>
            <h3 class="amber--text">Pantalla</h3>
            <v-checkbox
              style="margin-bottom: -1.5rem"
              color="amber darken-4"
              v-for="tamanio in tamanios"
              :key="tamanio"
              :label="`${tamanio}`"
            >
            </v-checkbox>
          </v-container>
        </v-card>
      </v-navigation-drawer>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "Precio",

  data: () => ({
    rules: [
      (value) => !!value || "Required.",
      (value) => (value && value.length >= 3) || "Min 3 characters",
    ],

    items: ["Fecha", "Precio"],
    opcion: "",
    drawer: false,
    group: null,
    marcas: [
      "iPhone",
      "Samsung",
      "Huawei",
      "OnePlus",
      "Xiaomi",
      "Oppo",
      "LG",
      "Vivo",
    ],
    sistemas: ["iOS", "Android"],
    tamanios: ['5"', '5,5"', '6"', '6,5"', '7"'],
  }),
  watch: {
    group() {
      this.drawer = false;
    },
  },
};
</script>

<style lang="scss" scoped></style>
