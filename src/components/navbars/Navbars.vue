<template>
<div>
<NavbarGrande></NavbarGrande>
<NavbarChiquito></NavbarChiquito>
</div>
 
</template>

<script>
  import NavbarGrande from './NavbarGrande.vue'
//  import NavbarChiquito from './NavbarChiquito.vue'
  export default {
      name: "Plantilla",
      components: {
        NavbarGrande,
      },
    data: () => ({
      links: [
        'Dashboard',
        'Messages',
        'Profile',
        'Updates',
      ],
    })
  }
</script>