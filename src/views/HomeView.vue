<template>
      <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 60 ? 'warm' : ''">
    <main>
      <div class="search-box">
        <input 
        type="text" 
        class="search-bar" 
        placeholder="  Search city to 'vue' the weather..."
        v-model="query"
        @keypress="fetchWeather"
        />
        <button id="Celcius" @click="fetchCelcius">Celcius</button>
        <button id="Fahrenheit" @click="fetchFahrenheit">Fahrenheit</button>
      </div>
      <BarChart />
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.state }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°F</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
      
    </main>
  </div>
</template>


<script>



export default {

  name: 'app',
  data () {

    return {
      api_key: '0d6bc458e9ae5b63dcaeea603d7c6d31',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },



  methods: {

    fetchWeather (e) {
    if (e.key == "Enter") {
      fetch(`${this.url_base}weather?q=${this.query}&units=imperial&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
    }
  },

  fetchCelcius () {
    fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
  },

  fetchFahrenheit () {
      fetch(`${this.url_base}weather?q=${this.query}&units=imperial&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
    },


  setResults (results) {
    this.weather = results;
  },
  dateBuilder () {
    let d = new Date();
    let months = ["January", "Febuary", "March", "April", "May", "June", "July", 
    "August", "September", "October", "November", "December"];
    let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

    let day = days[d.getDay()];
    let date = d.getDate();
    let month = months[d.getMonth()];
    let year = d.getFullYear();

    return `${day} ${date} ${month} ${year}`;
  }
}}
</script>

