<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
// importo axios
import axios from "axios";

// todo
export default {
  components: { AppHeader, AppMain },

  methods: {
    fetchCard() {
      axios
        .get("https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0")
        .then((response) => {
          const cardData = response;
          console.log(cardData);
        });
    },
    // inserisci i metodi
  },

  created() {
    // esegui alla creazione
    this.fetchCard();
  },
};
</script>

<template>
  <div class="">
    <AppHeader />
    <AppMain />
  </div>
</template>

<style lang="scss">
@use "./assets/styles/general.scss";
</style>
