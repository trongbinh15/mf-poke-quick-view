<template>
  <div
    class="flex flex-col space-x-2 text-sm bg-blue-300 border-l-0 font-light w-full sm:w-[400px] max-h-screen overflow-auto h-[500px] p-5 items-center space-y-3 rounded-sm shadow-lg"
  >
    <h1>Preview</h1>
    <div v-if="hasData" class="space-y-2">
      <div class="text-center">{{ displayName }}</div>
      <div class="p-1 bg-white rounded-lg shadow-md">
        <img
          v-lazy="{ src: getImageUrl(selectedPokemon.id), loading: spinner }"
          class="w-[96px] h-[96px] mx-auto"
        />
      </div>
      <div class="flex flex-col my-8 mx-auto space-y-4 w-[150px]">
        <HeightWeightComponent
          :height="selectedPokemon.height"
          :weight="selectedPokemon.weight"
        />
        <TypeComponent :types="selectedPokemon.types" />
        <StatComponent :stats="selectedPokemon.stats" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { computed, onMounted, reactive } from "vue";
import spinner from "../assets/Spinner-1s-96px.gif";
import HeightWeightComponent from "./HeightWeightComponent.vue";
import TypeComponent from "./TypeComponent.vue";
import StatComponent from "./StatComponent.vue";
const selectedPokemon = reactive({} as any);
onMounted(() => {
  window.addEventListener("pokemon-selected", async (e: any) => {
    if (e.detail && e.detail.length > 0) {
      const data = await getPokemonInfo(e.detail);
      if (data) {
        Object.assign(selectedPokemon, data);
      }
    }
  });
});

const hasData = computed(() => {
  return Object.keys(selectedPokemon).length > 0;
});

const displayName = computed(() => {
  const text = selectedPokemon.name as string;
  if (text && text.length > 0) {
    return text
      .split("-")
      .map((item) => item.charAt(0).toUpperCase() + item.slice(1))
      .join(" ");
  } else {
    return "";
  }
});

const getPokemonInfo = async (name: string) => {
  try {
    const response = await fetch("https://pokeapi.co/api/v2/pokemon/" + name);
    const data = await response.json();
    return data;
  } catch (error) {
    return null;
  }
};
const getImageUrl = (id: string) => {
  return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${id}.png`;
};
</script>
