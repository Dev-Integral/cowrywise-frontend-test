<template>
  <div class="modal-container">
    <div class="modal-content" v-bind:class="{ hide: !show }">
      <div class="close-icon" @click="emitClose">
        <i class="fa fa-times"></i>
      </div>
      <transition name="image">
        <div class="img-holder" v-if="show">
          <img :src="modalData.regular" alt="large" />
        </div>
      </transition>
      <transition name="image" appear>
        <div class="details" v-if="show">
          <h3>{{ modalData.first_name }} {{ modalData.last_name }}</h3>
          <p>{{ modalData.location }}</p>
        </div>
      </transition>
    </div>
    <transition name="modalImage" appear>
      <div v-if="!show" class="modal-content" v-bind:class="{ hide: show }">
        <div class="img-holder loading-background">
          <div class="loading-text">
            <p>Please wait</p>
            <div v-bind:class="{ loading: !show }"></div>
          </div>
        </div>
        <div class="details"></div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "ImageModal",
  props: ["modalData"],
  emits: ["close"],
  data() {
    return { show: false };
  },
  mounted() {
    setTimeout(() => (this.show = true), 2000);
  },
  methods: {
    emitClose(){
      this.show = false;
      this.$emit('close');
    }
  }
};
</script>

<style lang="scss">
@import '../assets/scss/colors';
.image-enter-from{
  opacity: 0;
  transform: scale(0);
}
.image-enter-to{
  opacity: 1;
  transform: scale(1);  
}
.image-enter-active{
  transition: all 1s ease;
}
.image-leave-from{
  opacity: 1;
}
.image-leave-to{
  opacity: 0;
}
.image-leave-active{
  transition: all 1s ease;
}
.scaleUp-enter-from {
  opacity: 0;
  transform: scale(0.5);
}
.scaleUp-enter-to {
  opacity: 1;
  transform: scale(1);
}
.scaleUp-enter-active {
  transform: all 1s ease;
}
.scaleUp-leave-from {
  opacity: 1;
  // transform: scale(1);
}
.scaleUp-leave-to {
  opacity: 0;
  // transform: scale(0.5);
}
.scaleUp-leave-active {
  transition: all 1s ease;
}

.hide {
  display: none;
}
.modal {
  &-container {
    position: absolute;
    bottom: 0;
    top: 0;
    left: 0;
    right: 0;
    background: #898989;
    background-color: rgba(20, 20, 20, 0.7);
    height: 255vh;
    z-index: 10;
  }
  &-content {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 15;
    width: 100%;
    height: 100%;
    max-width: 80vw;
    max-height: 90vh;
    .close-icon {
      color: white;
      float: right;
      font-weight: normal;
      opacity: 0.5;
      margin-right: 30px;
      margin-bottom: 20px;
    }
  }
}
.img-holder {
  width: 70%;
  height: 80%;
  padding: 0;
  margin: 0 auto;
  margin-top: 20px;
  border-radius: 10px 10px 0 0;

  img {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px 10px 0 0;
    border: none;
  }
}

.details {
  background: white;
  border: none;
  margin: 0 auto;
  border-radius: 0 0 10px 10px;
  width: 70%;
  h3,
  p {
    margin: 0;
    text-transform: capitalize;
    padding-left: 60px;
    color: $primary;
  }
  h3 {
    padding-top: 30px;
  }
  p {
    padding-bottom: 20px;
    padding-top: 10px;
  }
}

// PLEASE WAIT
@keyframes buttonLoadingSpinner {
  from {
    transform: rotate(0turn);
  }
  to {
    transform: rotate(1turn);
  }
}
.loading-background {
  background: $secondary;
  border-radius: 10px;
}
.loading-text {
  position: absolute;
  display: flex;
  align-items: center;
  top: 35%;
  left: 45%;
  color: $primary;
  justify-content: center;

  p {
    margin-left: 8px;
    color: $primary;
  }
}

.loading::after {
  content: "";
  position: absolute;
  width: 100px;
  height: 100px;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  border: 4px solid transparent;
  border-top-color: $primary;
  border-right-color: $primary;
  border-radius: 50%;
  animation: buttonLoadingSpinner 1s linear infinite;
}
// TRANSITION
.modalImage-enter-from {
  opacity: 0;
}
.modalImage-enter-to {
  opacity: 1;
}
.modalImage-enter-active {
  transition: all 1s ease;
}
.modalImage-leave-from {
  opacity: 1;
}
.modalImage-leave-to {
  opacity: 0;
}
.modalImage-leave-active {
  transition: all 1s ease;
}



// RESPONSIVENESS
@media only screen and (max-width: 767px) {
  .modal-container {
    height: 300vh;

    .img-holder {
      width: 100%;
    }
    .details {
      width: 100%;
    }
    .loading-text {
      left: 40%;
    }
  }
}
@media only screen and (min-width: 400px) {
  .modal-container{
    height: 400vh;
  }
}
@media only screen and (max-width: 565px) {
  .modal-container {
    height: 450vh;
    .loading-text {
      left: 30%;
    }
    .details {
      p,
      h3 {
        padding-left: 20px;
      }
    }
  }
}
</style>