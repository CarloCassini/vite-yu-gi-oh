<script>
import { store } from "../data/store";
export default {
  data() {
    return {
      store,
    };
  },
};
</script>

<template>
  <section>
    <div class="container">
      <div class="select-box">
        <select
          class="form-select form-select-lg mb-3"
          aria-label="Large select example"
        >
          <option selected>Open this select menu</option>
          <option value="1">One</option>
          <option value="2">Two</option>
          <option value="3">Three</option>
        </select>
      </div>

      <div v-for="(card, index) in store.cards">
        {{ index + 1 }} {{ card.name }} // {{ card.archetype }} //
        <img :src="card.card_images[0].image_url_small" alt="" />
        {{ card.card_images[0].image_url_small }}
      </div>
    </div>
  </section>
</template>

<style scoped>
section {
  background-color: #d48f38;
}
.select-box {
  width: 20%;
}
</style>
