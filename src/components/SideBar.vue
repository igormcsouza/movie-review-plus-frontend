<template>
  <nav>
    <v-app-bar app class="green lighten-3">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title class="text-uppercase" aling="center">
        <span class="font-weight-light">movie</span>
        <strong>review</strong>
      </v-toolbar-title>
      <!-- <v-spacer></v-spacer>
      <v-btn text>
        <span>Sign Out</span>
        <v-icon right>exit_to_app</v-icon>
      </v-btn> -->
    </v-app-bar>

    <v-navigation-drawer app v-model="drawer" class="green lighten-4">
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">{{ title }}</v-list-item-title>
          <v-list-item-subtitle>{{ subtitle }}</v-list-item-subtitle>
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
            <v-list-item-title>Version {{version}}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
const { version, title, subtitle } = require('../../package.json')

export default {
  data() {
    return {
      drawer: false,
      drawer_items: [
        { to: "/", icon: "mdi-view-dashboard", text: "Dashboard" },
        { to: "/about", icon: "mdi-help-box", text: "About" }
      ],
      version: version,
      title: title,
      subtitle: subtitle
    };
  }
};
</script>

<style>
</style>