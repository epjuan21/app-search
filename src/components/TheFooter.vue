<template>
  <v-footer dark app>
    <div class="caption">
      {{ new Date().getFullYear() }} — Desarrollado con Vue y Vuetify por
      <strong>Juan Fernando Ramírez</strong>
    </div>
    <v-spacer></v-spacer>
    <v-btn
      class="mx-4 white--text"
      icon
      href="https://twitter.com/epjuan"
      target="_blank"
    >
      <v-icon size="24px">mdi-twitter</v-icon>
    </v-btn>
    <v-btn
      class="mx-4 white--text"
      icon
      href="https://github.com/epjuan21"
      target="_blank"
    >
      <v-icon size="24px">mdi-github-circle </v-icon>
    </v-btn>
  </v-footer>
</template>
<script>
export default {
  data() {
    return {
      footerIcons: {
        icons: ["mdi-twitter", "mdi-github-circle"],
        links: ["https://twitter.com/?lang=es", "https://github.com/epjuan21"]
      }
    };
  }
};
</script>
