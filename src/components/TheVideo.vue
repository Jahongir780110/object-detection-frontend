<template>
  <div class="container video-processing">
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

      <div class="col-6 choose-video">
        <FileUpload type="video" />
      </div>

      <div class="col-6 result-video">
        <video controls>
          <source
            src="../assets/mixkit-lunch-between-a-man-and-a-woman-43998-medium.mp4"
            type="video/mp4"
          />
          Your browser does not support the video tag.
        </video>
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
.video-processing {
  height: 100%;
  position: relative;
}

.video-processing .row {
  height: 100%;
}

.video-processing .back-btn {
  position: absolute;
  top: 24px;
  left: 0;
  padding-left: 0;
}
.video-processing .back-btn svg {
  cursor: pointer;
  transition: 0.2s;
  fill: #fff;
}
.video-processing .back-btn svg:hover {
  fill: #fb1f79;
}

.choose-video {
  display: flex;
  align-items: center;
}

.result-video {
  display: flex;
  align-items: center;
  justify-content: center;
}

.result-video video {
  width: 100%;
  border-radius: 6px;
}
</style>
