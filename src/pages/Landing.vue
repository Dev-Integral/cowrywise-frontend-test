<template>
  <div class="landing-banner-container">
    <div class="searchbox-holder">
      <div class="fa-search-holder"><i class="fa fa-search"></i></div>
      <input
        type="text"
        placeholder="Search for photo"
        @change="searchTerm"
        v-model="searchText"
      />
    </div>
  </div>
  <div v-if="imageList && !loading">
    <Images
      v-on:showModal="imageData"
      v-bind:loading="loading"
      v-bind:imageList="imageList"
    />
  </div>
  <div v-else>
    <Loader/>
  </div>
  <div v-if="showModal">
    <ImageModal />
  </div>
</template>

<script>
import Images from "../components/Images.vue";
import ImageModal from "../components/Images.vue";
import Loader from "../components/Loader.vue";

export default {
  name: "Landing",
  emits: ["searchTerm", "setLoadingToFalse"],
  props: ["imageList", "loading"],
  components: { Images, ImageModal, Loader },
  data() {
    return {
      searchText: "",
      showModal: false,
      modalData: {},
    };
  },
  methods: {
    imageData(data) {
      this.$emit("setLoadingToFalse");
      this.modalData = data;
      this.showModal = true;
      console.log(this.modalData);
    },
    searchTerm() {
      this.$emit("searchTerm", this.searchText);
    },
  },
};
</script>

<style lang="scss">
.landing {
  &-banner-container {
    background: #dde2e9;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 200px;
    .searchbox-holder {
      display: flex;
      align-items: center;
      background: #fff;
      height: 30px;
      width: 80vw;
      padding: 5px 15px;
      border-radius: 8px;
      box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.05),
        0 6px 20px 0 rgba(0, 0, 0, 0.005);

      .fa-search-holder {
        margin-right: 10px;
        color: #dde2e9;
      }
      input {
        width: 100%;
        border: none;
        outline: none;
      }
      ::-webkit-input-placeholder {
        /* Edge */
        color: #253858;
      }

      :-ms-input-placeholder {
        /* Internet Explorer 10-11 */
        color: #253858;
      }

      ::placeholder {
        color: #253858;
        font-weight: bold;
      }
    }
  }
}
</style>