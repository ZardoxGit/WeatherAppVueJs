import Vue from 'vue'

import ResetInput from 'v-reset-input'

Vue.use(ResetInput)

<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Rechercher" v-model="cities" @keypress="weatherInfos"/>
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}</div>
          <div class="date">{{ currentDate() }}</div>
        </div>
      
        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
          <div class="weather">{{ weather.weather[0].description }}</div>
        </div>
      </div>
    </main>
  </div>
  
</template>

<script>
export default {
  name: "App",
  data () {
    return {
      api_key: "43a97c01ee587826f1cf74c5564bfb3a",
      url_base: "https://api.openweathermap.org/data/2.5/",
      cities: "",
      weather: {}
    }
  },
  methods: {
    weatherInfos (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.cities}&units=metric&appid=${this.api_key}&lang=fr`)
        .then(res => {
          return res.json();
        })
        .then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results;
    },
  
      currentDate() {
        var today = new Date();
        var days = ["Dimanche", "Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi", "Samedi"];
        var months = ["Janvier", "Février", "Mars", "Avril", "Mai", "Juin", "Juillet", "Aout", "Septembre", "Octobre", "Novembre", "Décembre"];
        var date = `${days[today.getDay()]} ${today.getDate()} ${months[today.getMonth()]} ${today.getFullYear()}`;
        
        return date;
      }

    
  }
}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;900&display=swap');

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Roboto', sans-serif;
    
  }

  #app {
    background-image: url('./assets/sky.jpg');
    background-size: cover;
    background-position: bottom;
  }
  main {
    min-height: 100vh;
    padding: 25px;
  }
  .search-box .search-bar {
    display: block;
    width: 100%;
    padding: 15px;
    text-align: center;
    background: none;
    border: none;
    outline: none;
    background-color:rgb(255, 255, 255, 0.50);
    border-radius: 20px;
    font-size:20px;
  }

  .weather-wrap {
    text-align: center;
    margin-top: 30px;

  }

  .location {
    font-size: 40px;
    color:white;
    text-shadow: 2px 2px 2px black;
    font-weight: 900;
  }

  .date {
    margin:10px;
    color:white;
    text-shadow: 2px 2px 2px black;
  }

  .temp {
    margin: 50px;
    font-family: 'Roboto', sans-serif;
    font-weight: 900;
    font-size: 100px;
    color: white;
    text-shadow: 2px 2px 2px black;
    background-color: rgb(255, 255, 255, 0.50);
    padding: 20px;
    border-radius: 100px;
    box-shadow: 2px 2px 2px black;
  }
  .weather {
    font-family: 'Roboto', sans-serif;
    font-weight: 900;
    font-size: 50px;
    color: white;
    text-shadow: 2px 2px 2px black;
    background-color: rgb(255, 255, 255, 0.50);
    padding: 15px;
    border-radius: 10px 40px;
    box-shadow: 2px 2px 2px black;
  }
  

</style>
