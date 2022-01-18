<template>
  <div class="landing-banner-container" v-if="showInputField">
    <transition name="slide-in-out">
      <div class="searchbox-holder" v-if="!loading">
        <div class="fa-search-holder"><i class="fa fa-search"></i></div>
        <input
          type="text"
          placeholder="Search for photo"
          @change="searchTerm"
          v-model="searchText"
        />
      </div>
    </transition>
  </div>
  <div v-else class="landing-banner-container">
    <transition name="slide-in-out" appear>
    <div class="results">
      <div class="icon-container" @click="defaultState"><i class="fa fa-arrow-left" aria-hidden="true"></i></div>
      <h2>
        Search Results for <span class="text">{{ `"${searchText}"` }}</span>
      </h2>
    </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "search",
  props: ["loading"],
  emits: ["searchTerm"],
  data() {
    return {
      searchText: "",
      showInputField: true,
    };
  },
  methods: {
    searchTerm(e) {
      e.preventDefault();
      this.showInputField = false;
      this.$emit("searchTerm", this.searchText);
    },
    defaultState(){  
        this.showInputField=true;
        this.searchText='';
        this.$emit("searchTerm", this.searchText);

    }
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/colors";
.landing {
  &-banner-container {
    background: $background;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 200px;
    .searchbox-holder {
      display: flex;
      align-items: center;
      background: $white;
      height: 40px;
      width: 80vw;
      padding: 5px 15px;
      border-radius: 8px;
      box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.05),
        0 6px 20px 0 rgba(0, 0, 0, 0.005);

      .fa-search-holder {
        margin-right: 10px;
        color: $background;
      }
      input {
        width: 100%;
        height: 40px;
        border: none;
        outline: none;
      }
      ::-webkit-input-placeholder {
        /* Edge */
        color: $primary;
      }

      :-ms-input-placeholder {
        /* Internet Explorer 10-11 */
        color: $primary;
      }

      ::placeholder {
        color: $primary;
        font-weight: bold;
      }
    }
    .results {
      display: flex;
      justify-content: center;
      align-items: center;
      color: $primary;
      font-size: 30px;
      .icon-container{
          margin-right: 20px;
      }
      .text {
        color: $search;
      }
    }
  }
}
@media only screen and (max-width: 565px) {
 
 .landing-banner-container .results{
        font-size: 20px;
    }
}
</style>