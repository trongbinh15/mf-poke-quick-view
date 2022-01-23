<template>
  <QuickView />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import QuickView from "./components/QuickView.vue";

export default defineComponent({
  name: "App",
  components: {
    QuickView,
  },
});
</script>
<style>
* {
  font-family: "SuperLegendBoy";
}
</style>

