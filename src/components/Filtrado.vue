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
  </div>
</template>

<script>
export default {
  name: "Filtrado",
  data() {
    return {
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
    };
  },
};
</script>
