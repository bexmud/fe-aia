<template>
  <div class="gallery">
    <div class="gallery-panel" v-for="photo in photos" :key="photo.id">
      <img :src="photo.image" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Gallery",
  data() {
    return {
      photos: [],
      errors: [],
    };
  },
  mounted() {
    console.log(this.$route.query);
    axios
      .get("https://intense-island-05089.herokuapp.com/image", {
        params: this.$route.query,
      })
      .then((response) => {
        return (this.photos = response.data);
      })
      .catch((e) => {
        this.error.push(e);
      });
  },
};
</script>

<style>
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
  grid-gap: 1rem;
  max-width: 80rem;
  margin: 5rem auto;
  padding: 0 5rem;
}
.gallery-panel img {
  width: 90%;
  height: 22vw;
  object-fit: cover;
  border-radius: 1rem;
}
</style>