<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import BaseButton from "./components/BaseButton.vue";
import BaseSelect from "./components/BaseSelect.vue";

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

      offset: 0,
      newStringa: "",
    };
  },
  components: { AppHeader, AppMain, BaseButton, BaseSelect },

  methods: {
    changeOffset() {
      this.newStringa = store.apiUrl.slice(0, -1);
      this.newStringa = this.newStringa + this.offset;
    },

    fetchCard(callToApi) {
      store.loading = true;
      axios
        .get(callToApi)
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

          store.totalFound = cardsData.length;

          store.cards = cardsData;
        })

        // viene eseguito a un errore della chiamata
        .catch((error) => {
          console.error(error);
          store.cards = [];
        })

        // viene eseguito sempre
        .finally(() => {
          store.loading = false;
        });
    },

    getArchetypes() {
      store.loading = true;

      axios
        .get("https://db.ygoprodeck.com/api/v7/archetypes.php")
        .then((response) => {
          store.archetypes = response.data;
        })

        // viene eseguito a un errore della chiamata
        .catch((error) => {
          console.error(error);
          store.archetypes = [];
        })

        // viene eseguito sempre
        .finally(() => {
          store.loading = false;
        });
    },

    searchArchetype(type) {
      if (type) {
        this.newStringa =
          "https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=" + type;
      } else {
        this.newStringa = store.apiUrl;
      }

      this.fetchCard(this.newStringa);
    },

    Annulla() {
      this.offset = 0;
      this.changeOffset();
      this.fetchCard(this.newStringa);
    },
    goNext() {
      this.offset += 20;
      this.changeOffset();
      this.fetchCard(this.newStringa);
    },
    goPrev() {
      if (this.offset >= 20) {
        this.offset -= 20;
      }
      this.changeOffset();
      this.fetchCard(this.newStringa);
    },
    // inserisci i metodi
  },

  created() {
    // esegui alla creazione
    this.changeOffset();
    this.fetchCard(this.newStringa);
    this.getArchetypes();
  },
};
</script>

<template>
  <div class="">
    <!-- apploading è registrata globalmente su main.js -->
    <AppLoading v-if="store.loading == true" />

    <div class="container">
      <AppHeader />
      <BaseButton @cliccked-test="goPrev()" nome="indietro" />
      <BaseButton @cliccked-test="goNext()" nome="avanti" />
      <BaseButton @cliccked-test="Annulla()" nome="annulla" />
      <BaseSelect @cambio-Select="searchArchetype" />
    </div>
    <AppMain />
  </div>
</template>

<style lang="scss">
@use "./assets/styles/general.scss";
</style>
