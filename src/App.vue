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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
