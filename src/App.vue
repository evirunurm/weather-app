<template>
<header class="header header--fixed ">
  <h1 class="header__logo"><span class="blackfont">PING</span>weather</h1>
</header>
<main>
  <section class="weather-summary">
    <div class="summary-background filter--dark" />
    <div class="searchbar">
      <label class="location-label" for="location-input">Location</label>
      <div class="location-searchbar">
        <input class="location-searchbar__input" id="location-input" type="text" name="" value="Amste">
        <img class="location-searchbar__icon" src="" alt="">
      </div>
    </div>
    <div class="summary">
      <div class="left">
        <p class="summary__today font--light">Today: </p>
        <h3 class="summary__cityname" id="weather_city-name">City Name</h3>
        <p class="summary__timedate font--light" id="weather_time-date">19:16 03/10</p>
        <h2 class="summary__degrees" id="weather_degrees">28</h2>
      </div>
      <div class="right">
        <div class="summary__icon__container">
          <img class="summary__icon" src="./assets/images/icons/001lighticons-01.svg" alt="">
        </div>

      </div>
    </div>
    <a class="summary-credits credits font--light" href="https://www.vecteezy.com/free-vector/nature">Nature Vectors by Vecteezy</a>
  </section>
  <section class="weather-details">
    <p class="weather-credits credits font--light">WeatherApi</p>
    <article class="forecast">
      <div class="article__title">
        <h3>Forecast</h3>
        <SeeMore />
      </div>
      <div class="forecast__content">
        <forecast-day />
      </div>
    </article>
    <article class="air">
      <div class="article__title">
        <h3>Air</h3>
        <SeeMore />
      </div>
      <div class="air__content">
        <div class="air__content__realfeel">
          <p class="light-font">RealFeel</p>
          <p class="" id="realFeel">30º</p>
        </div>
        <div class="air__content__uvindex">
          <p class="light-font">UVIndex</p>
          <p class="" id="uvIndex">Low</p>
        </div>
        <div class="air__content__wind">
          <p class="light-font">Wind</p>
          <p class="" id="wind">12 - 28 km/h</p>
        </div>
        <div class="air__content__humidity">
          <div class="humidity__data">
            <p class="light-font">Humidity</p>
            <p class="" id="humidity">80%</p>
          </div>
          <div class="humidity__graph">
            <div class="humidity__graph__container">
              <img class="humidity__graph__wave" src="" alt="">
              <img class="humidity__graph__drop" src="" alt="">
            </div>
          </div>
        </div>
      </div>
    </article>
    <hr>
    <article class="sunrise-sunset">
      <div class="article__title">
        <h3>Sunrise & Sunset</h3>
        <SeeMore />
      </div>
      <sunrise-sunset-graph />
      <div class="sunrise-sunset__data">
        <div class="sunrise-sunset__data__sunrise">
          <p class="light-font">Sunrise</p>
          <p id="humidity">8:06</p>
        </div>
        <div class="sunrise-sunset__data__sunset">
          <p class="light-font">Sunset</p>
          <p id="humidity">19:45</p>
        </div>
      </div>
    </article>

  </section>
</main>
<footer>
  <a href="http://www.freepik.com">Icons Designed by Freepik</a>
</footer>
</template>

<script>
import ForecastDay from './components/forecast_day.vue'
import SunriseSunsetGraph from './components/sunrise_sunset_graph.vue'
import SeeMore from './components/see_more.vue'

export default {
  name: 'App',
  data() {
    return {
      apiKey: 'helloimakey',
      searchQuery: '',
      apiUrl: 'http://api.weatherapi.com/v1/'
    }
  },
  methods: {},
  components: {
    ForecastDay,
    SunriseSunsetGraph,
    SeeMore
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;500;600;700;800&display=swap');

:root {
  --black: #0a0a0a;
  --white: #ffffff;
  --green: #D6F4DB;
  --blue: #91B0EE;
  --transparent: rgba(#ffffff, 0);
  --margin-border: 1.5rem;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  text-decoration: none;
  font-family: 'Open Sans', sans-serif;
}

body {
  overflow-x: hidden;
  background-color: pink;
}

/* ****** */
/* HEADER */
/* ****** */

.header {
  height: ;
  background-color: var(--white);
  width: 100%;
  display: flex;
  z-index: 10;
  align-items: center;
  position: fixed;
}

.header__logo {
  font-size: 1.5rem;
  padding: calc(var(--margin-border)/2) 0 calc(var(--margin-border)/2) var(--margin-border);
  font-weight: 300;

}

.blackfont {
  font-weight: 900;
}

/* ******* */
/* SUMMARY */
/* ******* */

.weather-summary {
  position: relative;
  padding-top: calc(var(--margin-border) + 2em);

  /* height: 45vh; */
}

.weather-summary>* {
  color: var(--white);
}

.summary-background {
  background-image: url(./assets/images/evening.svg);
  background-position: center;
  filter: brightness(50%);
  background-size: cover;
  width: 100%;
  height: 150%;
  position: absolute;
  top: 0;
  z-index: -10;
  color: inherit;
}

/* SEARCHBAR */
.searchbar {
  display: flex;
  flex-direction: column;
  padding: calc(var(--margin-border)/5) var(--margin-border) 0 var(--margin-border);
  color: var(--white);
}

.searchbar>p {
  color: var(--white);
}

.location-label {
  font-size: 0.75em;

}

.location-searchbar__input {
  background-color: var(--transparent);
  border: none;
  border-bottom: 1px solid var(--white);
  width: 100%;
  font-size: 0.75em;
  padding: 5px;
  color: var(--white);
}

.location-searchbar__input:focus {
  outline: none;
  background-color: rgb(255, 255, 255, 0.1);
}

/* SUMMARY */
.summary {
  padding: var(--margin-border) var(--margin-border) var(--margin-border) var(--margin-border);
  display: flex;
  justify-content: space-between;
}

.right {
  max-width: 50%;
}

.summary__icon {
  width: 100%;
  transform: scale(200%);
  padding-left: 15px;
  filter: invert(1) brightness(200%);
}

.summary__icon__container {
  overflow: hidden;
}

.summary-credits {
  padding: 0 0 0 var(--margin-border);
}

/* IMAGE CREDITS */


.credits {
  color: var(--white);
  font-size: 0.75em;
}



.font--light {
  font-weight: 100;
  opacity: 55%;
}

/* ******* */
/* DETAILS */
/* ******* */

.weather-details {
  background-color: var(--white);
  border-radius: 20px 20px 0 0;
  padding: 0.25em var(--margin-border) 0 var(--margin-border);
  z-index: 10;
}

.weather-credits {
  color: var(--black);
  padding: 0 0 0.5em 0
}

/* FORECAST */

.article__title {
  display: flex;
  justify-content: space-between;
  height: 2em;
  font-size: 0.75em;
}
</style>
