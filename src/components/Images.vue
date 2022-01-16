<template>
  <div class="grid-images">
    <div class="one">One</div>
    <div class="two">Two</div>
    <div class="three">Three</div>
    <div class="four">Four</div>
    <div class="five">Five</div>
    <div class="six">Six</div>
  </div>
</template>


<script>
import axios from 'axios';

export default {
  name: "Images",
  data(){
      return({info: '',})
  },
  mounted () {
    axios
      .get('https://api.unsplash.com/photos?count=6')
      .then(response => {
          console.log(response);
          this.info = response})
  }
};
</script>

<style lang="scss" scoped>
.grid-images {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
  grid-auto-rows: minmax(100px, auto);
  width: 80vw;
  margin: 0 auto;
  position: relative;
  bottom: 40px;

  .one {
    background: red;
  }
}
</style> scoped>
