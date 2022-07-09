<script>
export default {
  props: {
    stopRec: Function,
    playPauseVideo: Function,
    video: String,
    showVideo: Boolean,
  },
};
</script>

<template>
  <div class="ques_con">
    <div class="abc">
      <div class="ques_num">Question number 1</div>
    <div class="ques">Why are you the right person for the job?</div>
    </div>
    <div class="btn_con">
      <button :disabled="this.video || !this.showVideo" @click="this.stopRec">Start / Stop recording</button>
      <button :disabled="!this.video" @click="this.playPauseVideo">Play / Pause Recording</button>
    </div>
  </div>
</template>

<style>
.ques_con {
  width: 460px;
  align-self: stretch;
  padding: 26px 35px;
  display:flex;
  flex-direction: column;
}

.abc {
  flex:1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}

.ques_num {
  font-size: 14px;
  font-weight: 300;
}

.ques {
  margin-top: 39px;
  font-size: 30px;
  font-weight: 600;
}

.btn_con {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 35px;
}

.btn_con button {
  color: #ffffff;
  background-color: #b9bcc0;
  border-radius: 5px;
  font-size: 12px;
  font-weight: 600;
  border: none;
  letter-spacing: -0.340909px;
  padding: 8px 0px;
  width: 180px;
  cursor: pointer;
}

.btn_con button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

@media (max-width: 1280px) {
  .ques_con {
    width:unset;
  }

  .ques {
    margin-top: 24px;
    font-size: 20px;
    margin-bottom: 24px;
  }

  .btn_con {
    flex-direction: column;
    gap:0.75rem;
  }
}
</style>
