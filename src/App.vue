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
        <input list="locations" @input="fetchLocation(); fetchWeather();" class="location-searchbar__input" id="location-input" type="text" name="" v-model="location">
        <datalist id="locations">
          <option v-for="location in locationData" :value="location?.name" />
        </datalist>
        <img class="location-searchbar__icon" src="./assets/images/icons/search.png" alt="">
      </div>
    </div>
    <div class="summary">
      <div class="left">
        <p class="summary__today font--light">Today: </p>
        <h3 class="summary__cityname" id="weather_city-name">{{ weatherData?.location?.name }}</h3>
        <p class="summary__timedate font--light" id="weather_time-date">{{ weatherData?.location?.localtime }}</p>
        <div class="summary__degrees">
          <h2 class="degrees__number" id="weather_degrees">{{ weatherData?.current?.temp_c }}</h2>
          <p class="degrees__unit">ºC</p>
        </div>
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
        <forecast-day day="0" :weatherToday="forecastToday" />
        <forecast-day day="1" :weatherToday="forecastTomorrow" />
        <forecast-day day="2" :weatherToday="forecastAfter" />
      </div>
    </article>
    <article class="air">
      <div class="article__title">
        <h3>Air</h3>
        <SeeMore />
      </div>
      <div class="air__content__wraper">
        <div class="air__content ">
          <p class="font--light">RealFeel</p>
          <p class="" id="realFeel">{{ Math.round(weatherData?.current?.feelslike_c) }}ºC</p>
        </div>
        <div class="air__content humidity">
          <p class="font--light">UVIndex</p>
          <p v-if="(weatherData?.current?.uv < 4)" id="uvIndex">Low</p>
          <p v-if="(weatherData?.current?.uv <= 6 && weatherData?.current?.uv >= 4)" id="uvIndex">Medium</p>
          <p v-if="(weatherData?.current?.uv > 6)" id="uvIndex">High</p>
        </div>
        <div class="air__content humidity">
          <p class="font--light">Wind</p>
          <p class="" id="wind">{{ weatherData?.current?.wind_kph }} km/h</p>
        </div>
        <div class="air__content humidity">
          <div class="humidity__data">
            <p class="font--light">Humidity</p>
            <p class="" id="humidity">{{ weatherData?.current?.humidity }}%</p>
          </div>
          <humidity-graph :humidity=weatherData?.current?.humidity />
          <!-- weatherData?.current?.humidity -->
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
      <div class="sunrise-sunset__data__wrapper">
        <div class="sunrise-sunset__data">
          <p class="font--light">Sunrise</p>
          <p id="humidity">{{ weatherData?.forecast?.forecastday[0]?.astro?.sunrise }}</p>
        </div>
        <div class="sunrise-sunset__data">
          <p class="font--light">Sunset</p>
          <p id="humidity">{{ weatherData?.forecast?.forecastday[0]?.astro?.sunset }}</p>
        </div>
      </div>
    </article>

  </section>
</main>
<footer>
  <a href="http://www.freepik.com">Icons Designed by Freepik</a>
  <p>Designed by </p>
</footer>
</template>

<script>
import ForecastDay from './components/forecast_day.vue'
import SunriseSunsetGraph from './components/sunrise_sunset_graph.vue'
import SeeMore from './components/see_more.vue'
import HumidityGraph from './components/humidity_graph.vue'


export default {
  name: 'App',
  props: {
    location: String,
  },
  data() {
    return {
      apiKey: '2c9b7c40a56942f6ace143344210410',
      // 2c9b7c40a56942f6ace143344210410,
      apiUrl: 'http://api.weatherapi.com/v1/',
      locationData: [],
      weatherData: {},
      forecastToday: {},
      forecastTomorrow: {},
      forecastAfter: {},
    }
  },
  methods: {
    async fetchLocation() {
      if (this.location.length > 2) {
        const url = `${this.apiUrl}search.json?key=${this.apiKey}&q=${this.location}`;
        try {
          const response = await fetch(url, {
            mode: "cors",
          });
          const responseJson = await response.json();
          console.log(responseJson)

          this.locationData = responseJson;
        } catch (error) {
          console.log(error)
        }
      }
    },
    async fetchWeather() {
      console.log("not fetching yet")
      this.locationData.forEach(async (item, i) => {
        if (item.name == this.location) {
          const url = `${this.apiUrl}forecast.json?key=${this.apiKey}&q=${item.name}&days=3&aqi=no&alerts=no`;
          try {
            const response = await fetch(url, {
              mode: "cors",
            });
            this.weatherData = await response.json();
            this.divideForecast();
          } catch (error) {
            console.log(error);
          }
        }
      });
    },
    divideForecast() {
      console.log(this.weatherData.forecast.forecastday[0])
      this.forecastToday = this.weatherData.forecast.forecastday[0];
      this.forecastTomorrow = this.weatherData.forecast.forecastday[1];
      this.forecastAfter = this.weatherData.forecast.forecastday[2];
    },
  },
  components: {
    ForecastDay,
    SunriseSunsetGraph,
    SeeMore,
    HumidityGraph,
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

.location-searchbar {
  position: relative;
}

.location-searchbar__icon {
  position: absolute;
  height: 90%;
  right: 7%;
}

/* SUMMARY */
.summary {
  padding: var(--margin-border) var(--margin-border) var(--margin-border) var(--margin-border);
  display: flex;
  justify-content: space-between;
}

.summary__cityname {
  font-weight: normal;
  font-size: 1.5em;
}

.summary__degrees {
  font-size: 1.5em;
  display: flex;
  align-items: center;
}

.degrees__number,
.degrees__unit {
  font-size: 3em;
  font-weight: 600;
}

.degrees__unit {
  font-size: 1.5em;
  transform: translateY(-20%);
}

.right {
  max-width: 50%;
  display: flex;
  align-items: center;
}

.summary__icon {
  width: 100%;
  transform: scale(225%);
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
}

article {
  margin: calc(var(--margin-border)/2) 0 calc(var(--margin-border)/2) 0;
}

/* FORECAST */

.article__title {
  display: flex;
  justify-content: space-between;
  height: 2em;
  font-size: 0.75em;
}

.forecast {
  margin-top: calc(var(--margin-border)/6);
}

/* AIR */

.air__content__wraper {
  display: grid;
  grid-auto-flow: column;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  font-size: 0.75em;
  margin: calc(var(--margin-border)/2) 0 0 0;
}

.air__content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  height: 2em;
  font-weight: 500 !important;
}

.humidity__data {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr 1fr;
}

.humidity__graph {
  display: flex;
  justify-content: flex-end;
}

/* SUNRISE AND SUNSET */

.sunrise-sunset__data__wrapper {
  font-weight: 500 !important;
  display: grid;
  grid-auto-flow: column;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;
  font-size: 0.75em;
  margin: calc(var(--margin-border)/2) 0 0 0;
}

.sunrise-sunset__data {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;
  justify-content: space-between;
}

.sunrise-sunset__data:nth-last-child(1) {
  text-align: right;
}

/* ****** */
/* FOOTER */
/* ****** */

footer {
  font-size: 0.75em;
  opacity: 0.5;
  margin: var(--margin-border) 0 var(--margin-border) var(--margin-border);
}

footer a {
  color: var(--black);
}

/* AIR */
</style>
