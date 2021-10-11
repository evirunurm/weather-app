<template>
<div class="sunrise-sunset__graph">
  <div class="graph__divisor" />
  <div class="graph__divisor" />
  <div class="graph__divisor" />
  <div class="graph__divisor" />
  <div id="sunsetSunriseData" class="graph__data" />
</div>
<div class="graph__hours font--light">
  <p>00:00</p>
  <p>06:00</p>
  <p>12:00</p>
  <p>18:00</p>
  <p>00:00</p>
</div>
</template>

<script >
export default {
  props: {
    astro: {}
  },
  methods: {
    changeData() {
      const sunsetSunriseData = document.getElementById("sunsetSunriseData");

      let sunset24 = this.transformTimeMetric(this.astro.sunset);
      let sunrise24 = this.transformTimeMetric(this.astro.sunrise);
      let dayTime = this.getDayTime(sunset24, sunrise24);

      sunsetSunriseData.style.width = `${(dayTime * 100) / 24}%`;
      sunsetSunriseData.style.left = `${(this.translateTimeFloat(sunrise24)* 50) / 12}%`;
    },
    transformTimeMetric(time) {
      let withoutFormat = time.split(" ")[0];
      let hours = parseInt(withoutFormat.split(":")[0]);
      let minutes = parseInt(withoutFormat.split(":")[1]);

      if (time.includes("PM")) {
        hours += 12;
      }
      return {
        hours,
        minutes
      };
    },
    getDayTime(sunset, sunrise) {
      let minutes;
      let hours = sunset.hours - sunrise.hours;
      if (sunset.minutes - sunrise.minutes < 0) {
        hours--;
        minutes = 60 + (sunset.minutes - sunrise.minutes);
      } else {
        minutes = sunset.minutes - sunrise.minutes;
      }

      return this.translateTimeFloat({
        hours,
        minutes
      });
    },
    translateTimeFloat(time) {
      time.minutes = 60 / time.minutes;
      return parseFloat(`${time.hours}.${time.minutes}`);
    },
  },
  updated() {
    this.changeData();
  },
  mounted() {
    this.changeData();
  }
};
</script>

<style scoped>
.sunrise-sunset__graph {
  position: relative;
  width: 100%;
  height: 70px;
  margin: calc(var(--margin-border)/2) 0 0 0;
  display: grid;
  border-radius: 10px 10px 10px 10px;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr;
  overflow: hidden;
}

.graph__divisor {
  border: 1px solid rgba(0, 0, 0, 0.5);
  border-right: 0;
  z-index: 20;
}

.graph__divisor:nth-child(1) {
  border-radius: 10px 0 0 10px;
}

.graph__divisor:nth-last-child(2) {
  border-radius: 0 10px 10px 0;
  border: 1px solid rgba(0, 0, 0, 0.5);
}

.graph__data {
  background-color: var(--green);
  position: absolute;
  transform: translate();
  height: 100%;
}

.graph__hours {
  display: flex;
  justify-content: space-between;
  font-size: 0.75em;
  font-weight: normal;
  margin-top: 0.25em;
}
</style>
