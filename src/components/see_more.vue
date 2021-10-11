<template>
<a href="https://www.weatherapi.com/weather/">
  <p>SEE MORE</p>
  <svg width="6px" height="10">
    <line x1="0" y1="0" x2="6" y2="5" style="stroke:black;stroke-width:1" />
    <line x1="6" y1="5" x2="0" y2="10" style="stroke:black;stroke-width:1" />
  </svg>
</a>
</template>

<script >
export default {

};
</script>

<style scoped>
a {
  color: var(--black);
  opacity: 50%;
  display: flex;
  align-items: baseline;
}

p {
  padding-right: 1em;
}
</style>
