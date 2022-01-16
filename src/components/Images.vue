<template>
  <div class="grid-images" v-if="ImageData">
    <!-- <div class="one"></div>
    <div class="two">Two</div>
    <div class="three">Three</div>
    <div class="four">Four</div>
    <div class="five">Five</div>
    <div class="six">Six</div> -->
    <div
      class="application-item"
      v-for="(image, index) in ImageData"
      v-bind:key="index"
      @click="$emit('showModal', image)"
    >
      <div>
        <img v-bind:src="image['thumb']" />
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";

export default {
  name: "Images",
  data() {
    return { ImageData: [] };
  },
  async beforeMount() {
    await axios
      .create({
        headers: {
          Authorization: `Client-ID estcMmHOEb9W3QUAoPQqjpEP_YhBJI7v7ey8RCtnJhE`,
        },
      })
      .get("https://api.unsplash.com/photos?limit=6")
      .then((response) => {
        let data = response.data;
        data.forEach((element, index) => {
          index < 6 ?this.ImageData.push({...element.urls, ...element.user }) : null;
        });
        console.log(this.ImageData);

        return this.ImageData;
      });
  },
};
</script>

<style lang="scss" scoped>
.grid-images {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
	border-radius: 10px;
  gap: 10px;
  width: 80vw;
  margin: 0 auto;
  position: relative;
  bottom: 40px;

  .one {
    background: red;
  }
}
</style> scoped>
