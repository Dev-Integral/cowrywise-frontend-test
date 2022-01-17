<template>
  <div class="modal-container">
    <div class="modal-content" v-bind:class="{ hide: !show }">
      <div class="close-icon" @click="$emit('close')">
        <i class="fa fa-times"></i>
      </div>
      <div class="img-holder">
        <img :src="modalData.raw" alt="large" />
      </div>
      <div class="details">
        <h3>{{ modalData.first_name }} {{ modalData.last_name }}</h3>
        <p>{{ modalData.location }}</p>
      </div>
    </div>
    <div class="modal-content" v-bind:class="{ hide: show }">
      <div class="img-holder loading-background">
        <div class="loading-text">
          <p>Please wait</p>
          <div v-bind:class="{ loading: !show }"></div>
        </div>
      </div>
      <div class="details"></div>
    </div>
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
    setTimeout(() => (this.show = true), 5000);
  },
};
</script>

<style lang="scss">
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
    height: 155vh;
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
    color: #253858;
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
  background: #ddd;
}
.loading-text {
  position: absolute;
  display: flex;
  align-items: center;
  top: 35%;
  left: 45%;
  color: #fff;
  justify-content: center;

  p {
    margin-left: 8px;
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
  border-top-color: #eee;
  border-right-color: #ddd;
  border-radius: 50%;
  animation: buttonLoadingSpinner 1s linear infinite;
}
@media only screen and (max-width: 767px) {
  .modal-container {
    height: 200vh;

    .img-holder {
      width: 100%;
    }
    .details{
      width: 100%;
    }
    .loading-text {
      left: 40%;
    }
  }
}
@media only screen and (max-width: 565px) {
  .modal-container {
    height: 300vh;
    .loading-text {
      left: 30%;
    }
    .details{
      p, h3{
        padding-left: 20px;
      }
    }
  }
}
</style>