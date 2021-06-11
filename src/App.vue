<template>
  <v-app class="app">
    <v-main class="app">
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>
<style lang="scss" scoped>
.app {
  background: #161616;
  height: 100%;
  width: 100%;
}
</style>
