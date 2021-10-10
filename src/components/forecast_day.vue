<template>
<div class="forecast__day">
  <div class="left">
    <div class="forecast__day__icon__conatiner">
      <img class="forecast__day__icon" src="../assets/images/icons/001lighticons-01.svg" :alt="weatherToday?.day?.condition?.text">
    </div>
    <p v-if="day == '0'" class="forecast__day__text">Today</p>
    <p v-else-if="day == '1'" class="forecast__day__text">Tomorrow</p>
    <p v-else class="forecast__day__text">{{ transformDate(weatherToday?.date) }}</p>
  </div>
  <p class="forecast__day__text">{{Math.round(weatherToday?.day?.mintemp_c)}} / {{Math.round(weatherToday?.day?.maxtemp_c)}}</p>
</div>
<hr>
</template>

<script >
export default {
  props: {
    weatherToday: {},
    day: String,
  },
  methods: {
    transformDate(date) {
      if (date && date.includes("-")) {
        let transformedDate = "";
        const noYear = date.replace("2021-", " ");
        let month = noYear.split("-")[0];
        let monthText;
        switch (parseInt(month)) {
          case 1:
            monthText = "Jan";
            break;
          case 2:
            monthText = "Feb";
            break;
          case 3:
            monthText = "Mar";
            break;
          case 4:
            monthText = "Apr";
            break;
          case 5:
            monthText = "May";
            break;
          case 6:
            monthText = "Jun";
            break;
          case 7:
            monthText = "Jul";
            break;
          case 8:
            monthText = "Aug";
            break;
          case 9:
            monthText = "Sep";
            break;
          case 10:
            monthText = "Oct";
            break;
          case 11:
            monthText = "Novr";
            break;
          case 12:
            monthText = "Dec";
            break;
          default:
            monthText = month;
        }
        transformedDate = `${monthText} ${noYear.split("-")[1]}`
        return transformedDate;
      }
      return date;
    }
  }
};
</script>

<style scoped>
.forecast__day {
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

.forecast__day__text {}

.left {
  display: flex;
  align-items: center;
  gap: 1em;
}
</style>
