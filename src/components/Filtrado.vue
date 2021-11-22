<template>
  <div>
    <!--class="d-none d-lg-flex d-xl-flex d-md-flex"-->
    <v-card elevation="3" class="d-none d-lg-flex d-xl-flex d-md-flex">
      <v-container
        style="padding-left: 1.4rem; margin-bottom: 1rem; padding-right: 5rem"
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
            v-for="marca in checkmarca"
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
          v-for="sistema in checksistemas"
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
  </div>
</template>

<script>
//import {db} from './../db';
export default {
  name: "Filtrado",
  data() {
    return {
      marcas: [],
      sistemas: [],
      pantallas: [],
      switch1: false,
      productos: [],
      checkmarca: [
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
  computed: {
    // filtro por categorias y rango de precios
    selectedItems: function () {
      return this.productos.filter(function (newProductos) {
        if (
          this.marcas.length > 0 ||
          this.pantallas.length > 0 ||
          this.sistemas.length > 0
        ) {
          if ((this.marcas.length > 0) & (this.pantallas.length > 0)) {
            return (
              this.marcas.includes(newProductos.marca) &
              this.pantallas.includes(newProductos.pantalla) &
              (this.switch1 === newProductos.nuevo) &
              ((newProductos.precio >= this.range[0]) &
                (newProductos.precio <= this.range[1]))
            );
          } else if ((this.marcas.length > 0) & (this.sistemas.length > 0)) {
            return (
              this.marcas.includes(newProductos.marca) &
              this.sistemas.includes(newProductos.sistema) &
              (this.switch1 === newProductos.nuevo) &
              ((newProductos.precio >= this.range[0]) &
                (newProductos.precio <= this.range[1]))
            );
          } else if ((this.sistemas.length > 0) & (this.pantallas.length > 0)) {
            return (
              this.sistemas.includes(newProductos.sistema) &
              this.pantallas.includes(newProductos.pantalla) &
              (this.switch1 === newProductos.nuevo) &
              ((newProductos.precio >= this.range[0]) &
                (newProductos.precio <= this.range[1]))
            );
          } else {
            return (
              (this.marcas.includes(newProductos.marca) ||
                this.sistemas.includes(newProductos.sistema) ||
                this.pantallas.includes(newProductos.pantalla)) &
              (this.switch1 === newProductos.nuevo) &
              ((newProductos.precio >= this.range[0]) &
                (newProductos.precio <= this.range[1]))
            );
          }
        } else {
          return (
            !this.marcas.includes(newProductos.marca) &
            !this.sistemas.includes(newProductos.sistema) &
            !this.pantallas.includes(newProductos.pantalla) &
            (this.switch1 === newProductos.nuevo) &
            ((newProductos.precio >= this.range[0]) &
              (newProductos.precio <= this.range[1]))
          );
        }
      }, this);
    },
  },
};
</script>
