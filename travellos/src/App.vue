<template>
  <div id="app">
    <h1>Travellos</h1>
    <search-bar></search-bar>
    <places-list v-model="places"></places-list>
  </div>
</template>

<script>
import SearchBar from "./components/SearcBar";
import PlacesList from "./components/PlacesList";
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
    "search-bar": SearchBar,
    "places-list": PlacesList
  }
};
</script>

<style>

  body {
  background-image: url("/background.webp");
  background-size: cover;
  background-attachment: fixed;
  font-family: cursive;
}

h1 {
  text-align: center;
  color: rgb(13, 94, 13);
  margin-top: 4%;
}
</style>