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
      callToApi: "",
      offset: 0,
      newStringa: "",
    };
  },
  components: { AppHeader, AppMain },

  methods: {
    changeOffset() {
      this.newStringa = this.callToApi.slice(0, -1);
      this.newStringa = this.newStringa + this.offset;
      console.log(this.newStringa);
    },

    fetchCard(callToApi) {
      console.log("we" + callToApi);
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
          store.paginationNext = "";
          store.paginationPrev = "";
        })

        // viene eseguito sempre
        .finally(() => {
          store.loading = false;
        });
    },

    goNext() {
      console.log("vado next");
      this.offset += 20;
      this.changeOffset();
      this.fetchCard(this.newStringa);
    },
    goPrev() {
      console.log("vado next");
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
    this.callToApi = store.apiUrl;
    this.changeOffset();
    this.fetchCard(this.newStringa);
  },
};
</script>

<template>
  <div class="">
    <!-- apploading è registrata globalmente su main.js -->
    <button type="button" class="btn btn-primary ms-5" @click="goNext()">
      avanti
    </button>
    <button type="button" class="btn btn-primary ms-5" @click="goPrev()">
      indietro
    </button>
    <AppLoading v-if="store.loading == true" />
    <AppHeader />
    <AppMain />
  </div>
</template>

<style lang="scss">
@use "./assets/styles/general.scss";
</style>
