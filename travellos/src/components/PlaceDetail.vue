<template>
  <div class="place">
    <div class="image-container">
      <img :src="place.images[0].source_url" alt="No image found" v-if="place.images.length > 0" />
      <img src="/not_found.png" v-else />
    </div>
    <div clas="place-information">
      <div class="place-price">
        <a :href="getPlaceLink(place)" target="_blank">{{place.name}}</a>
      </div>
      <div class="place-snippet">
        <p>{{place.snippet.slice(0, 150) + "..."}}</p>
      </div>
      <div>
        <button class="show-location" v-on:click="toggleShowMap()">Show Location</button>
        <div :class="showMap ? 'show' : 'hide'">
          <div :id="place.id" class="map"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "place-detail",
  props: ["place"],
  data() {
    return {
      showMap: false
    };
  },
  mounted() {
    const latitude = this.place.coordinates.latitude;
    const longitude = this.place.coordinates.longitude;
    const map = L.map(this.place.id).setView([latitude, longitude], 12);
    L.tileLayer(
      "https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}",
      {
        attribution:
          'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="http://mapbox.com">Mapbox</a>',
        maxZoom: 18,
        id: "mapbox.streets",
        accessToken:
          "pk.eyJ1IjoiYmxhY2ttb3JlMCIsImEiOiJjaXlub251ZjIwMDJmMnBxems2bmpiYXA2In0.2Hxl5QoDhIY6OR4p3GsU2w"
      }
    ).addTo(map);

    L.marker([latitude, longitude])
      .addTo(map)
      .bindPopup(`This is ${this.place.name}.`);
  },
  methods: {
    getPlaceLink: function(place) {
      const result = this.place.attribution.find(
        attribution => attribution.source_id === "wikipedia"
      );
      if (result !== undefined) {
        return result.url;
      } else {
        return this.place.attribution[0].url;
      }
    },
    toggleShowMap: function() {
      this.showMap = !this.showMap;
    }
  }
};
</script>

<style>
.map {
  width: 10vw;
  height: 15vh;
}

.show {
  visibility: visible;
}

.hide {
  visibility: hidden;
}

.place {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 17rem;
  margin: 0 0.5rem 2.3rem 0.5rem;
}

.image-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow: hidden;
  background: #000;
}

.image-container img {
  width: 100%;
}

.place .image-container {
  height: 15rem;
  margin-bottom: 1rem;
}

.place h2 {
  margin-bottom: 0.5rem;
  font-size: 1.2rem;
  font-weight: 600;
}

.place-information {
  display: flex;
  justify-content: space-between;
}

.place-information p {
  font-size: 1.2rem;
  line-height: 1.5rem;
}

.place-snippet {
  min-height: 10em;
}

.show-location {
  width: 40%;
  padding: 10px;
  background: #03bfc5;
  color: white;
  font-size: 12px;
  border: 1px solid #03bfc5;
  border-radius: 8px;
  cursor: pointer;
}

.show-location:hover {
  background: #12dfdf;
}
</style>