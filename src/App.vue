<script setup>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";

// export default {
//   components: { AppHeader, AppMain },
// };
</script>

<template>
  <div class="debug">
    <AppHeader />
    <AppMain />
  </div>
</template>

<style lang="scss">
@use "./assets/styles/general.scss";
</style>
