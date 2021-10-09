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

};
</script>

<style scoped>
.sunrise-sunset__graph {
  position: relative;
  /* background: red; */
  width: 100%;
  height: 70px;
  margin: calc(var(--margin-border)/2) 0 0 0;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr;
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
  width: 50%;
  height: 100%;
  left: 60px;
}

.graph__hours {
  display: flex;
  justify-content: space-between;
  font-size: 0.75em;
  font-weight: normal;
  margin-top: 0.25em;
}
</style>
