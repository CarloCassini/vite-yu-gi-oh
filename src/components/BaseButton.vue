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
    {{ nome }}
  </button>
</template>

<style scoped></style>
