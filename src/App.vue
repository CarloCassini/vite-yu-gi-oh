<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
// importo axios
import axios from "axios";

// importare store
// bisogna importarlo con le grafe perchè ha bisogno del destructuring
import { store } from "./data/store";

// todo
export default {
  data() {
    return {
      store,
    };
  },
  components: { AppHeader, AppMain },

  methods: {
    fetchCard() {
      store.loading = true;

      axios
        .get(store.apiUrl)
        .then((response) => {
          // questo codice viene esequito se la chiamata all'API rende 200 e va a buon fine
          const cardsData = response.data.data.map((card) => {
            const { id, name, archetype, card_images } = card;
            return {
              id,
              name,
              archetype,
              cardImage: card_images[0].image_url_small,
            };
          });
          store.cards = cardsData;
        })

        // viene eseguito a un errore della chiamata
        .catch((error) => {
          console.error(error);
          store.cards = [];
          store.paginationNext = "";
          store.paginationPrev = "";
        })

        // viene eseguito sempre
        .finally(() => {
          store.loading = false;
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
