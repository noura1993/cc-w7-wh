<template>
<div class="wrapper">
  <div class="search-bar">
    <input type="text" placeholder="Enter country name..." v-model="country" />
    <button v-on:click="searchForCountry()">
      <i class="fa fa-search"></i>
    </button>
  </div>
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
      fetch(
        `https://www.triposo.com/api/20200405/poi.json?location_id=${this.country}&count=50&account=${this.account}&token=${this.api_token}`
      )
        .then(response => response.json())
        .then(jsonResponse => eventBus.$emit("search-results", jsonResponse));
    }
  }
};
</script>

<style>

.wrapper {
    text-align: center;
}

.search-bar {
  margin-top: 1%;
}

.search-bar input {
  padding: 10px;
  font-size: 17px;
  border: 1px solid #fff;
  border-radius: 8px;
  width: 25%;
  background: #f1f1f1;
  /* text-align: center; */
}

.search-bar button {
  width: 3%;
  padding: 10px;
  background: #03bfc5;
  color: white;
  font-size: 18px;
  border: 1px solid #03bfc5;
  border-radius: 8px;
  cursor: pointer;
}

.search-bar button:hover {
  background: #12dfdf;
}

</style>