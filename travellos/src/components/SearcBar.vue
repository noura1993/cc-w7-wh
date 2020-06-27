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
      account: process.env.VUE_APP_ACCOUNT,
      api_token: process.env.VUE_APP_API_TOKEN,
      country: ""
    };
  },

  methods: {
    searchForCountry: function() {
      fetch(`https://www.triposo.com/api/20200405/poi.json?location_id=${this.country}&count=50&account=${this.account}&token=${this.api_token}`)
      .then(response => response.json())
      .then(jsonResponse =>  eventBus.$emit("search-results", jsonResponse));
    }
  }
};
</script>

<style>
</style>