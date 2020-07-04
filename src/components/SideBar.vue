<template>
  <nav>
    <v-app-bar app class="green lighten-3">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title class="text-uppercase" aling="center">
        <span class="font-weight-light">movie</span>
        <strong>review</strong>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text>
        <span>Sign Out</span>
        <v-icon right>exit_to_app</v-icon>
      </v-btn>
    </v-app-bar>

    <v-navigation-drawer app v-model="drawer" class="green lighten-4">
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">Movie Review Plus</v-list-item-title>
          <v-list-item-subtitle>A sweet upgrade</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav>
        <!-- Routes -->
        <v-list-item v-for="item in drawer_items" :key="item.text" router :to="item.to">
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>{{ item.text }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title>Version 2.0.0</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
      drawer_items: [
        { to: "/", icon: "mdi-view-dashboard", text: "Dashboard" },
        { to: "/about", icon: "mdi-help-box", text: "About" }
      ]
    };
  }
};
</script>

<style>
</style>