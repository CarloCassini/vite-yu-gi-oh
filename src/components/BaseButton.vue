<script>
export default {
  props: {
    nome: String,
  },

  emits: ["cliccked-test"],
};
</script>

<template>
  <button
    type="button"
    class="btn btn-primary mx-3"
    @click="$emit('cliccked-test')"
  >
    <!-- questa sintassi mi permette di avere un valore di default cliccami se non dovesse arrivare nulla dalle props -->
    {{ nome || "cliccami" }}
  </button>
</template>

<style scoped></style>
