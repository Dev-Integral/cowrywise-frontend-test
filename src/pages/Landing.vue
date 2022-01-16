<template>
  <div class="landing-banner-container">
    <div class="searchbox-holder">
      <div class="fa-search-holder"><i class="fa fa-search"></i></div>
      <input type="text" placeholder="Search for photo" />
    </div>
  </div>
  <Images />
</template>

<script>
import Images from "../components/Images.vue";
export default {
  name: "Landing",
  components: { Images },
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
      width: 90vw;
      padding: 5px 15px;
      border-radius: 8px;

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