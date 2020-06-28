<template>
  <div>
    <div class="places-list">
      <place-detail v-for="place in places.slice(1, this.count)" :key="place" :place="place"></place-detail>
    </div>
    <div class="show-more">
      <button class="show-more-button" v-on:click="increaseCount()" v-if="places.length !== 0 && this.count < 100">Show more</button>
    </div>
  </div>
</template>

<script>
import PlaceDetail from "./PlaceDetail";

export default {
  name: "places-list",
  props: ["places"],
  data() {
    return {
      count: 10
    };
  },
  methods: {
    increaseCount: function() {
      this.count += 10;
    }
  },
  components: {
    "place-detail": PlaceDetail
  }
};
</script>

<style>
.places-list {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  margin: 4.4rem 10%;
}

.show-more {
  text-align: center;
}

.show-more-button {
  width: 10%;
  padding: 10px;
  background: #03bfc5;
  color: white;
  font-size: 18px;
  border: 1px solid #03bfc5;
  border-radius: 8px;
  margin-bottom: 2%;
  cursor: pointer;
}

.show-more-button:hover {
  background: #12dfdf;
}

</style>