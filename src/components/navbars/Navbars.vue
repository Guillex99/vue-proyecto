<template>
  <NavbarGrande></NavbarGrande>
</template>

<script>
import NavbarGrande from "./NavbarGrande.vue";
//  import NavbarChiquito from './NavbarChiquito.vue'
export default {
  name: "Navbars",
  components: {
    NavbarGrande,
  },
  data: () => ({
    links: ["Dashboard", "Messages", "Profile", "Updates"],
  }),
};
</script>
