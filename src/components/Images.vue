<template>
<div>
  <div class="grid-images">
    <div
      class="item"
      v-for="(image, index) in imageList"
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
	
</div>
</template>


<script>
// import Loader from './Loader.vue';
export default {
  name: "Images",
  emits: ["showModal"],
	props: ["imageList", "loading"],
	// components: {Loader},
  data() {
    return {  };
  }
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
  cursor: pointer;

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
    background: linear-gradient(to top, rgba(10, 32, 10, 0.4), transparent);
    position: absolute;
    bottom: 0;
    border-radius: 10px;
  }
}
.image-card:hover .veil {
  height: 100%;
  background: linear-gradient(to top, rgba(10, 32, 10, 0.9), transparent);
}
@media only screen and (max-width: 900px) {
  .grid-images {
    gap: 20px;
  }
  .image-card {
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
    bottom: 10%;
  }
  #item-3 {
    bottom: 0%;
    height: 100%;
  }
  #item-4 {
    bottom: 10%;
  }
  #item-5 {
    bottom: 0%;
  }
}
@media only screen and (max-width: 565px) {
  .grid-images, .loader-container {
    grid-template-columns: 1fr;
    gap: 10px;
  }
  #item {
    &-0 {
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
