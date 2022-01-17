<template>
  <div class="loader-container">
    <div v-for="(num, index) in numbersArray" :key="num">
      <div v-bind:id="`item-${index}`">
        <ContentLoader
          viewBox="0 0 450 400"
          backgroundColor="#f0f0f0"
          foregroundColor="#dedede"
        >
          <rect x="43" y="304" rx="4" ry="4" width="271" height="20" />
          <rect x="44" y="333" rx="4" ry="4" width="200" height="9" />
          <rect x="42" y="-170" rx="10" ry="10" width="400" height="407" />
        </ContentLoader>
      </div>
    </div>
  </div>
</template>

<script>
import { ContentLoader } from "vue-content-loader";
export default {
  name: "Loader",
  components: { ContentLoader },
  data() {
    return {
      numbersArray: [1, 2, 3, 4, 5, 6],
    };
  },
};
</script>

<style lang="scss" scoped>
.loader-container {
  position: relative;
  display: grid;
  width: 70vw;
  margin: 0 auto;
  gap: 30px;
  grid-template-columns: 1fr 1fr 1fr;
  z-index: 5;
}

@media only screen and (max-width: 900px) {
  .loader-container {
    gap: 20px;
  }
  #item-1 {
    height: 100%;
  }
}
@media only screen and (max-width: 767px) {
  .loader-container {
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
  .loader-container {
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
}
</style>