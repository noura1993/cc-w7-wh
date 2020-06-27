<template>
  <div id="app">
    <search-bar></search-bar>
  </div>
</template>

<script>
import SearchBar from "./components/SearcBar";
import { eventBus } from "./main";

export default {
  name: "App",
  data() {
    return {
      places: []
    };
  },

  mounted() {
    eventBus.$on("search-results", results => {
      this.places = results;
    });
  },

  components: {
    "search-bar": SearchBar
  }
};
</script>

<style>
</style>