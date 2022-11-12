<template>
  <div class="container camera-processing">
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

      <div class="col-6 toggle-camera">
        <button
          type="button"
          class="btn btn-outline-light"
          @click="toggleCamera"
        >
          {{ toggleButtonText }}
        </button>
      </div>

      <div class="col-6 result-video">
        <video v-if="isCameraTurnedOn" autoplay ref="camera">
          Your browser does not support the video tag.
        </video>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isCameraTurnedOn: false,
    };
  },
  computed: {
    toggleButtonText() {
      if (!this.isCameraTurnedOn) {
        return "Turn on camera";
      } else {
        return "Turn off camera";
      }
    },
  },
  methods: {
    goBack() {
      this.$router.back();
    },
    toggleCamera() {
      if (this.isCameraTurnedOn) {
        return this.turnOffCamera();
      }

      const constraints = {
        audio: false,
        video: true,
      };
      navigator.mediaDevices
        .getUserMedia(constraints)
        .then((stream) => {
          this.isCameraTurnedOn = true;
          this.$nextTick(() => {
            this.$refs.camera.srcObject = stream;
          });
        })
        .catch(() => {
          alert("Please give access to camera");
        });
    },
    turnOffCamera() {
      const tracks = this.$refs.camera.srcObject.getTracks();

      tracks.forEach((track) => {
        track.stop();
      });

      this.isCameraTurnedOn = false;
    },
  },
};
</script>

<style scoped>
.camera-processing {
  height: 100%;
  position: relative;
}

.camera-processing .row {
  height: 100%;
}

.camera-processing .back-btn {
  position: absolute;
  top: 24px;
  left: 0;
  padding-left: 0;
}
.camera-processing .back-btn svg {
  cursor: pointer;
  transition: 0.2s;
  fill: #fff;
}
.camera-processing .back-btn svg:hover {
  fill: #fb1f79;
}

.toggle-camera {
  display: flex;
  align-items: center;
}

.toggle-camera button {
  width: 300px;
  font-size: 24px;
  background-color: #fb1f79;
  border-color: #fb1f79;
  color: #fff;
}
.toggle-camera button:hover {
  background-color: transparent;
  border-color: #fb1f79;
  color: #fb1f79;
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
