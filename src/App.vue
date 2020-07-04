<template>
  <v-app>
    <m-side-bar />
    <v-main>
      <v-card height="500" class="overflow-hidden main-card">
        <router-view></router-view>
      </v-card>
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

  data: () => ({
    //
  })
};
</script>

<style scoped>
.main-card {
  margin: 10px 50px;
  padding: 30px;
}
</style>
