<template>
  <div id="app">
    <div class="top-div">
      <h1>Travellos</h1>
      <search-bar></search-bar>
    </div>
    <places-list :places="places"></places-list>
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
  margin: 0;
  font-family: cursive;
}

.top-div {
  background-image: url("/background.webp");
  background-size: cover;
  background-attachment: fixed;
  width: 100%;
  height: 80vh;
}

h1 {
  text-align: center;
  color: rgb(13, 94, 13);
  margin-top: 0;
  padding-top: 6%;
}
</style>