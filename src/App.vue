<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import BaseButton from "./components/BaseButton.vue";

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
  components: { AppHeader, AppMain, BaseButton },

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
          console.log(store.archetypes[9].archetype_name);
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

    <!-- <button type="button" class="btn btn-primary ms-5" @click="goPrev()">
      indietro
    </button>
    <button type="button" class="btn btn-primary ms-5" @click="goNext()">
      avanti
    </button>
    <button type="button" class="btn btn-primary ms-5" @click="Annulla()">
      annulla
    </button> -->
    <div class="container">
      <AppHeader />
      <BaseButton @cliccked-test="goPrev()" nome="indietro" />
      <BaseButton @cliccked-test="goNext()" nome="avanti" />
      <BaseButton @cliccked-test="Annulla()" nome="annulla" />
    </div>
    <AppMain />
  </div>
</template>

<style lang="scss">
@use "./assets/styles/general.scss";
</style>
