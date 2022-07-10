<script>
export default {
  props: {
    counter: Number,
  },
};
</script>

<template>
  <div class="countdown_screen_con">
    <img class="mask" src="src/assets/images/mask.png" />
    <div class="counter">
      {{ this.counter }}
    </div>
    <i class="sentence">Take a deep breath...</i>
    
  </div>
</template>

<style>
.countdown_screen_con {
  position: absolute;
  background-color: #248291;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: url("src/assets/images/illustration.png");
  background-repeat: no-repeat;
  background-position: 50% 100%;
  background-size: auto 85%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.countdown_screen_con::after {
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1;
  background-color: rgba(0, 0, 0, 0.25);
  top: 0;
  left: 0;
}

.sentence {
  position: absolute;
  font-size: 16px;
  font-weight: 500;
  color: #ffffff;
  bottom: 40px;
  z-index: 2;
}

.mask {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    height: 43%;
    top:33%;
}

.counter {
  font-weight: 400;
  font-size: 100px;
  color: #ffffff;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2;
}

</style>
