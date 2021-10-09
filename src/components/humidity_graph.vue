<template>
<div class="humidity__graph">
  <div class="humidity__graph__container">
    <img class="humidity__graph__wave" src="../assets/images/humidity_wave.svg" alt="">
    <img class="humidity__graph__drop" src="../assets/images/humidity_drop.svg" alt="">
  </div>
</div>
</template>

<script >
export default {

};
</script>

<style scoped>
.humidity__graph__container {
  position: relative;
  overflow: hidden;
  height: 50px;
  width: 50px;
  border-radius: 7px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.humidity__graph__wave {
  position: absolute;
  transform: scale(120%);
  left: 12px;
  /* top: 0px; */
  z-index: 20;
  animation-name: wave;
  animation-duration: 4s;
  animation-iteration-count: infinite;
  animation-direction: alternate-reverse;
  animation-timing-function: cubic-bezier(0, 0);
}

.humidity__graph__drop {
  position: relative;
  z-index: 30;
  filter: drop-shadow(0 1px 5px rgba(0, 0, 0, 0.25));
}

@keyframes wave {
  from {
    left: 12px;
  }

  to {
    left: -77px;
  }
}
</style>
