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
    <div class="container bg-brown">
      <div class="select-box py-3"></div>
    </div>

    <div class="container">
      <!-- container per le card -->
      <div class="">
        <div class="row row-cols-5 justify-content-between">
          <div class="col my-2" v-for="(card, index) in store.cards">
            <div class="card">
              <img :src="card.cardImage" class="card-img-top" alt="..." />
              <div class="card-body">
                <h5 class="card-title">{{ card.name }}</h5>
                <p class="card-text">
                  {{ card.archetype }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.container {
  background-color: white;
  .card {
    background-color: #d48f38;
    text-align: center;
    height: 500px;
  }
  .card-title {
    margin-bottom: auto;
    color: white;
  }
}
.bg-brown {
  background-color: #d48f38;
}
section {
  background-color: #d48f38;
}
.select-box {
  width: 20%;
}
</style>
