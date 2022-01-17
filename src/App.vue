<template>
  <div id="App">
    <Landing
      v-bind:imageList="imageList"
      v-bind:loading="loading"
      v-on:searchTerm="searchTextFxn"
    />
  </div>
</template>

<script>
import Landing from "./pages/Landing.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Landing,
  },
  data() {
    return {
      imageList: null,
      loading: true,
    };
  },
  methods: {
    searchTextFxn(text) {
      return text
        ? this.getList(`https://api.unsplash.com/search/photos?&query=${text}`)
        : null;
    },
    async getList(link) {
      this.loading = false;

      await axios
        .create({
          headers: {
            Authorization: `Client-ID estcMmHOEb9W3QUAoPQqjpEP_YhBJI7v7ey8RCtnJhE`,
          },
        })
        .get(link)
        .then((response) => {
          let data = response.data;
          this.imageList = [];
          let initialData = [];

          if (data.results) {
            data.results.forEach((element, index) => {
              index < 6
                ? initialData.push({ ...element.urls, ...element.user })
                : null;
            });
          } else if(data) {
            data.forEach((element, index) => {
              index < 6
                ? initialData.push({ ...element.urls, ...element.user })
                : null;
            });
          }
          this.imageList = initialData;
          return this.imageList;
        })
        .catch((error) => {
          console.log({ error });
          this.loading = false;
        });
    },
  },
  async beforeMount() {
    this.getList(`https://api.unsplash.com/photos`);
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
  font-family: "Poppins";
}
</style>
