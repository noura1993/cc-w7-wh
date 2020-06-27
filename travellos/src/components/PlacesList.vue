<template>
  <div class="places-list">
    <place-detail v-for="place in places" :key="place"></place-detail>
  </div>
</template>

<script>
import PlaceDetail from "./PlaceDetail";

export default {
  name: "places-list",
  props: ["places"],
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
</style>