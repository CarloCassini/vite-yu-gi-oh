<script>
import { store } from "../data/store";
export default {
  data() {
    return {
      store,
    };
  },
  props: {},

  emits: [],
};
</script>

<template>
  <select
    class="form-select form-select-lg mb-3"
    aria-label="Large select example"
  >
    <option
      v-for="(archetype, index) in store.archetypes"
      :value="index"
      :key="index"
    >
      {{ archetype.archetype_name }}
    </option>
  </select>
</template>

<style scoped></style>
