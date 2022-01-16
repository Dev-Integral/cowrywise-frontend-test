<template>
  <div class="grid-images" v-if="ImageData">
    <div
      class="item"
      v-for="(image, index) in ImageData"
      v-bind:key="index"
      @click="$emit('showModal', image)"
    >
      <div class="image-card" :id="`item-${index}`">
        <img v-bind:src="image['small']" />
        <div class="veil"></div>
        <div class="user-details">
          <h4>{{ image.first_name }} {{ image.last_name }}</h4>
          <div>
            <p v-if="image.location">{{ image.location }}</p>
            <p v-else>N/A</p>
          </div>
        </div>
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
          index < 6
            ? this.ImageData.push({ ...element.urls, ...element.user })
            : null;
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
  grid-template-columns: 2fr 2fr 1fr;
  grid-template-columns: 1fr 1fr 1fr;
  border-radius: 10px;
  gap: 30px;
  width: 70vw;
  margin: 0 auto;
  position: relative;
  bottom: 40px;
}
#item-0 {
  height: 70%;
}
#item-2 {
  height: 80%;
}
#item-3 {
  bottom: 30%;
}
#item-5 {
  bottom: 20%;
}
.image-card {
  position: relative;
  height: 350px;

  img {
    margin: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px;
  }
  h4 {
    margin-bottom: 5px;
  }
  p {
    margin: 0;
  }
  .user-details {
    position: absolute;
    bottom: 20px;
    left: 20px;
    color: #fff;
    z-index: 5;
    width: 100%;
  }
  .veil {
    width: 100%;
    height: 40%;
    z-index: 3;
    background-color: transparent;
    // opacity: 0.8;
    background: linear-gradient(to top, rgba(10, 32, 10, 0.4), transparent);
    // background: linear-gradient(1deg, #000e 0.0005%, transparent);
    position: absolute;
    bottom: 0;
    border-radius: 10px;
  }
}
@media only screen and (max-width: 900px) {
  .grid-images {
    gap: 20px;
  }
  .image-card {
    height: 250px;
    h4 {
      margin: 0;
    }
    p {
      font-size: 13px;
    }
    .user-details {
      bottom: 10px;
      left: 10px;
    }
    #item-1 {
      height: 100%;
    }
  }
}
@media only screen and (max-width: 767px) {
  .grid-images {
    grid-template-columns: 1fr 1fr;
  }
  #item-0 {
    height: 80%;
  }
  #item-1 {
    height: 100%;
  }
  #item-2 {
    height: 100%;
    bottom: 18%;
  }
  #item-3 {
    bottom: 0%;
    height: 100%;
  }
  #item-4 {
    bottom: 20%;
  }
  #item-5 {
    bottom: 0%;
  }
}
@media only screen and (max-width: 565px) {
  .grid-images {
    grid-template-columns: 1fr;
    gap: 10px;
  }
  #item {
    &-0
   {
      height: 100%;
    }
  }
	#item-3 {
      height: 100%;
    }
  #item-4,
  #item-2 {
    bottom: 0;
  }
  #item {
    bottom: 0;
  }
}
</style>
