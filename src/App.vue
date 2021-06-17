<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Ville..." v-model="cities" @keypress="weatherInfos"/>
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
        var days = ["Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi", "Samedi", "Dimanche"];
        var months = ["Janvier", "Février", "Mars", "Avril", "Mai", "Juin", "Juillet", "Aout", "Septembre", "Octobre", "Novembre", "Décembre"];
        var date = `${days[today.getDay()]} ${today.getDate()} ${months[today.getMonth()]} ${today.getFullYear()}`;
        
        return date;
      }
    
  }
}
</script>

<style>

  @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

  * {
    margin:auto;
    box-sizing: border-box;
    font-family: 'Roboto';
  }

  .search-box .search-bar {
    width: 100%;
  }

  main {
    min-height: 100vh;
  }

  #app {
    background-image: url(./assets/sky.jpg);
    background-size:auto;
    background-position:center;
  }

</style>
