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
      axios
        .get("https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0")
        .then((response) => {
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
          // minuto 0:50
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
