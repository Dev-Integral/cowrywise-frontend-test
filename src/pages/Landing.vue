<template>
  <Search :loading="loading" v-on:searchTerm="searchTerm" />
  <div v-if="imageList && !loading">
    <Images
      v-on:showModal="imageData"
      v-bind:loading="loading"
      v-bind:imageList="imageList"
    />
  </div>
  <div v-else>
    <Loader />
  </div>
  <div v-if="showModal">
    <ImageModal
      v-bind:modalData="modalData"
      v-on:close="showModal = false"
      v-if="showModal"
    />
  </div>
</template>

<script>
import Images from "../components/Images.vue";
import ImageModal from "../components/ImageModal.vue";
import Loader from "../components/Loader.vue";
import Search from "../components/Search.vue";

export default {
  name: "Landing",
  emits: ["searchTerm"],
  props: ["imageList", "loading"],
  components: { Images, ImageModal, Loader, Search },
  data() {
    return {
      showModal: false,
      modalData: {},
    };
  },
  methods: {
    imageData(data) {
      this.modalData = data;
      this.showModal = true;
    },
    searchTerm(term) {
      console.log(term)
      this.$emit("searchTerm", term);
    },
  },
};
</script>

<style lang="scss">
// Slide-in-out
@import '../assets/scss/colors';

.slide-in-out-enter-active {
  animation: wobble 0.5s ease;
}

.slide-in-out-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.slide-in-out-leave-to {
  opacity: 0;
  transform: translateX(60px);
}
.slide-in-out-leave-active {
  transition: all 0.5s ease;
}
@keyframes wobble {
  0% {
    transform: translateY(-60px);
    opacity: 0;
  }
  50% {
    transform: translateY(0px);
    opacity: 1;
  }
  60% {
    transform: translateX(8px);
  }
  70% {
    transform: translateX(-8px);
  }
  80% {
    transform: translateX(4px);
  }
  90% {
    transform: translateX(-4px);
  }
  100% {
    transform: translateX(0);
  }
}
</style>