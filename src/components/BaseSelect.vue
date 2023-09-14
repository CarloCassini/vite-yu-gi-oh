<script>
import { store } from "../data/store";
export default {
  data() {
    return {
      store,
      term: "",
    };
  },

  methods: {
    annullaRicerca() {
      this.term = "";
    },
  },
  props: {},

  emits: ["cambio-Select", "annulla-ricerca"],
};
</script>

<template>
  <div class="bg-brown">
    <select
      class="form-select form-select-lg mt-5 mb-3"
      aria-label="Large select example"
      v-model="term"
      @change="$emit('cambio-Select', term)"
    >
      <option :value="''" selected>annulla ricerca</option>
      <option
        v-for="(archetype, index) in store.archetypes"
        :value="archetype.archetype_name"
        :key="index"
      >
        {{ archetype.archetype_name }}
      </option>
    </select>
    <span>totale righe trovate : {{ store.totalFound }}</span>
    <button
      type="button"
      class="btn btn-primary mx-3 mb-5"
      @click="$emit('annulla-ricerca')"
    >
      <!-- questa sintassi mi permette di avere un valore di default cliccami se non dovesse arrivare nulla dalle props -->
      {{ nome || "annulla ricerca" }}
    </button>
  </div>
</template>

<style scoped>
.bg-brown {
  background-color: burlywood;
}
</style>
