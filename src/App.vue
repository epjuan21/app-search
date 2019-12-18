<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app clipped left>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">
            Menú
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
          :to="item.route"
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app clipped-left>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title class="text-uppercase grey--text"
        >Buscador</v-toolbar-title
      >
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content>
      <router-view />
      <TheFooter />
    </v-content>
  </v-app>
</template>

<script>
import TheFooter from "@/components/TheFooter";

export default {
  components: {
    TheFooter
  },

  name: "App",

  data() {
    return {
      drawer: null,
      items: [
        { title: "Inicio", icon: "mdi-home", route: "/" },
        { title: "Invima", icon: "mdi-pill", route: "search-one" },
      ]
    };
  }
};
</script>

<style lang="scss" scoped>
.d-space-between {
  min-height: 100vh;
  display: flex;
  justify-content: space-between;
}
</style>
