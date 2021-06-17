<template>
  <div id='app'>
    <main>
      <div class='search-box'>
        <input type='text' class='search-bar' placeholder='Ville...' v-model="cities" @keypress="fetchWeather"/>
      </div>
      <div class='weather-wrap' >
        <div class='location-box'>
          <div class='location'>{{ weather.name }}</div>
          <div class='date'>{{ date() }}</div>
        </div>
      
        <div class='weather-box'>
          <div class='temp'>{{ weather.main.temp }}°C</div>
          <div class='weather'>Soleil</div>
        </div>
      </div>
    </main>
  </div>
  
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      api_key: '43a97c01ee587826f1cf74c5564bfb3a',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      cities: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key == 'Enter') {
        fetch(`${this.url_base}weather?q=${this.cities}&units=metric&appid=${this.api_key}`)
        .then(res => {
          return res.json();
        })
        .then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results;
    },
  
      date() {
        var today = new Date();
        var date = `${today.getDate()}/${today.getMonth()+1}/${today.getFullYear()}`;
        return date;
      }
    
  }
}
</script>

<style>
  
 
</style>
