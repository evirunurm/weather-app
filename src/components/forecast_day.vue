<template>
<div class="forecast__day">
  <div class="left">
    <div class="forecast__day__icon__conatiner">
      <img class="forecast__day__icon" src="../assets/images/icons/001lighticons-01.svg" alt="">
    </div>
    <p id="" class="forecast__day__text right">Today</p>
  </div>
  <p class="forecast__day__text">23º / 9º</p>
</div>
<hr>
</template>

<script >
export default {

};
</script>

<style scoped>
.forecast__day {
  /* background-color: pink; */
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5em 0 0.5em 0;
}

.forecast__day__icon__conatiner {
  overflow: hidden;
  height: 30px;
  display: flex;
}

.forecast__day__icon {
  transform: scale(200%);
}

.left {
  display: flex;
  align-items: center;
  gap: 1em;
}
</style>
