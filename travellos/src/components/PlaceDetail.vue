<template>
  <div class="place">
    <div class="image-container">
      <img :src="place.images[0].source_url" alt="No image found" />
    </div>
    <h2>{{place.name}}</h2>
    <div class="place-information">
      <div class="place-price">
        <p>{{place.price_tier}}</p>
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
  props: ["place"]
};
</script>

<style>
.place {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 16.66rem;
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
  font-size: 0.88rem;
  font-weight: 300;
  line-height: 1rem;
}
</style>