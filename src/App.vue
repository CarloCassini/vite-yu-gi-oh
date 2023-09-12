<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
// importo axios
import axios from "axios";

// todo
export default {
  data() {
    return {
      cards: [],
    };
  },
  components: { AppHeader, AppMain },

  methods: {
    fetchCard() {
      axios
        .get("https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0")
        .then((response) => {
          // console.log("vediamo " + response.data.data.name);
          // const cardsData = response.data.data.map((card) => {
          //   const { id, name, archetype, card_images } = card;
          //   return { id, name, archetype, card_images };
          // });
          // this.cards = cardsData;
          this.cards = response.data.data;

          // console.log("ciccio" + this.cards);
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
  <div v-for="(card, index) in cards" :key="card.id">
    {{ index + 1 }} - {{ card.name }}
  </div>
  <div class="">
    <AppHeader />
    <AppMain />
  </div>
</template>

<style lang="scss">
@use "./assets/styles/general.scss";
</style>
