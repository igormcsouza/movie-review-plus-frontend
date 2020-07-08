<template>
  <v-app>
    <m-side-bar />
    <v-main class="main">
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import MSideBar from "./components/SideBar";

export default {
  name: "App",

  components: {
    MSideBar
  },

  mounted: function() {
    let elHtml = document.getElementsByTagName("html")[0];
    elHtml.style.overflowY = "auto";
  },

  destroyed: function() {
    let elHtml = document.getElementsByTagName("html")[0];
    elHtml.style.overflowY = null;
  },

  data: () => ({
    //
  })
};
</script>