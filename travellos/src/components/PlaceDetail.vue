<template>
  <div class="place">
    <div class="image-container">
      <img :src="place.images[0].source_url" alt="No image found" v-if="place.images.length > 0"/>
      <img src="/not_found.png" v-else/>
    </div>
    <div clas="place-information">
      <div class="place-price">
        <a :href="getPlaceLink(place)" target="_blank"> {{place.name}} </a>
      </div>
      <div class="place-snippet">
        <p>{{place.snippet}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "place-detail",
  props: ["place"],
  methods: {
      getPlaceLink: function (place) {
        const result = this.place.attribution.find(attribution => attribution.source_id === "wikipedia");
        if(result !== undefined) {
            return result.url;
        }else {
            return this.place.attribution[0].url;
        }
      }
  }
};
</script>

<style>
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
  height: 10rem;
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
    min-height: 15em;
}
</style>