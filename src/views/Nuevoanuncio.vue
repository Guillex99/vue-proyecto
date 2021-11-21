<!--Vista para crear un anuncio-->
<template>
  <v-container>
    <v-row>
      <v-col>
        <Nuevoproducto></Nuevoproducto>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Nuevoproducto from "./../components/Nuevoproducto.vue";
export default {
  name: "Nuevoanuncio",
  components: {
    Nuevoproducto,
  },
};
</script>
