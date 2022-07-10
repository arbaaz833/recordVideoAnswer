<script>
import Question from "./QuesComponent.vue";
import CountDownScreen from "./CountDownScreen.vue";

export default {

  components:{
    Question,
    CountDownScreen
  },

  data() {
    return {
      showVideo: false,
      videoStream: null,
      recorder: null,
      counter: 5,
      videoTimer: 30,
      timerId: "",
      counterId: "",
      video: null,
      isVideoPlaying: false,
    };
  },
  mounted() {
    (async () => {
      try {
        let stream = await navigator.mediaDevices.getUserMedia({ audio: true, video: true });
        this.videoStream = stream;
        this.counterId = setInterval(() => {
          this.counter--;
        }, 1000);
        this.recorder = new MediaRecorder(stream);
      } catch (error) {}
    })();
  },
  methods: {
    stopRec() {
      clearInterval(this.timerId);
      this.recorder.stop();
      this.recorder.ondataavailable = (e) => {
        this.video = URL.createObjectURL(e.data);
      };
      this.videoStream = null;
    },
    playPauseVideo() {
      if (this.isVideoPlaying) {
        this.$refs.videoRef.pause();
      } else this.$refs.videoRef.play();
      this.isVideoPlaying = !this.isVideoPlaying;
    },
  },
  watch: {
    counter(newValue) {
      if (newValue === 0) {
        clearInterval(this.counterId);
        this.showVideo = true;
        this.recorder.start();
        this.timerId = setInterval(()=>{
          this.videoTimer--;
        },1000)
      }
    },
    videoTimer(timeLeft) {
      if(timeLeft===0){
        this.stopRec();
      }
    }
  },
};
</script>

<template>
  <div class="root">
    <div class="con">
      <div class="video_con">
        <div v-if="!video" class="timer_con">
          <div>00:{{videoTimer}}</div>
        </div>
        <video
          v-if="showVideo"
          class="video"
          ref="videoRef"
          :srcObject="videoStream"
          :autoplay="!video"
          :muted="!video"
          :src="video"
          @ended="() => (isVideoPlaying = false)"
        ></video>

        <div v-else>
          <CountDownScreen :counter="counter" />
        </div>
      </div>

      <Question :showVideo="showVideo" :video="video" :stopRec="stopRec" :playPauseVideo="playPauseVideo" :isVideoPlaying="isVideoPlaying" />

    </div>
  </div>
</template>

<style>
.root {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.con {
  max-width: 1320px;
  margin: 0px 3rem;
  display: flex;
  justify-content: center;
  flex: 1;
  border-radius: 10px;
  background-color: #FFFFFF;
  overflow: hidden;
}

.video_con {
  flex: 1;
  height: 480px;
  position: relative;
}

.timer_con {
  position: absolute;
  width: 100%;
  top: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1;
}

.timer_con > div {
  background: #1B2432;
  border-radius: 0px 0px 10px 10px;
  text-align: center;
  font-size: 18px;
  font-weight: 600;
  color: #FFFFFF;
  padding: 0px 40px;
}

.video {
  transform: rotateY(180deg);
  -webkit-transform: rotateY(180deg); /* Safari and Chrome */
  -moz-transform: rotateY(180deg); /* Firefox */
    position: absolute;
    top: 0;
    left: 0;
    object-fit: cover;
    width: 100%;
    height: 100%;
}

@media (max-width:1280px) {
  .con {
    flex-direction: column;
    margin: 1rem ;
    height: calc(100% - 2rem);
  }

  .video_con {
    height: unset;
  }

}
</style>
