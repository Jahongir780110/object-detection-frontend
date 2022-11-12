<template>
  <div class="container image-processing">
    <div class="row">
      <div class="back-btn text-white">
        <svg
          style="width: 42px; height: 42px"
          viewBox="0 0 24 24"
          @click="goBack"
        >
          <path
            d="M20,11V13H8L13.5,18.5L12.08,19.92L4.16,12L12.08,4.08L13.5,5.5L8,11H20Z"
          />
        </svg>
      </div>

      <div class="col-6 choose-image">
        <FileUpload type="image" />
      </div>

      <div class="col-6 result-image">
        <img
          src="https://www.treehugger.com/thmb/kaA2K_9wVzTbPIyCRm3-oZuy6k0=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/horse.primary-e9a47e1c486c4fb7bf729e05b59cf0df.jpg"
          alt="result image"
        />
      </div>
    </div>
  </div>
</template>

<script>
import FileUpload from "./FileUpload.vue";
export default {
  components: {
    FileUpload,
  },
  methods: {
    goBack() {
      this.$router.back();
    },
  },
};
</script>

<style scoped>
.image-processing {
  height: 100%;
  position: relative;
}

.image-processing .row {
  height: 100%;
}

.image-processing .back-btn {
  position: absolute;
  top: 24px;
  left: 0;
  padding-left: 0;
}
.image-processing .back-btn svg {
  cursor: pointer;
  transition: 0.2s;
  fill: #fff;
}
.image-processing .back-btn svg:hover {
  fill: #fb1f79;
}

.choose-image {
  display: flex;
  align-items: center;
}

.result-image {
  display: flex;
  align-items: center;
  justify-content: center;
}

.result-image img {
  width: 100%;
  border-radius: 6px;
}
</style>
