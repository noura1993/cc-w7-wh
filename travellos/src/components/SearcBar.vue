<template>
  <div>
    <input type="text" placeholder="Enter country name..." v-model="country" />
    <button v-on:click="searchForCountry()">
      <i class="fa fa-search"></i>
    </button>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  name: "search-bar",
  data() {
    return {
      country: ""
    };
  },

  methods: {
    searchForCountry: function() {
      eventBus.$emit("search-results", [{ name: "Castle" }]);
    }
  }
};
</script>

<style>
</style>