<template>
  <div>This is Quick View</div>
  <div>{{ selectedPokemon }}</div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
const selectedPokemon = ref("");
// eslint-disable-next-line @typescript-eslint/no-explicit-any
window.addEventListener("pokemon-selected", (e: any) => {
  selectedPokemon.value = e.detail;
});
</script>
