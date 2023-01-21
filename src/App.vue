<template>
  <div className = "container">
    <h1>Aplikacja Pogodowa</h1>
    <input v-model="city" placeholder="Wprowadź miasto" @keyup.enter="fetchWeatherData()">
    <p>{{ weatherData.description ? weatherData.description.toUpperCase() : 'N/A' }}</p>
    <p>Temperatura: {{ Math.round(weatherData.temp) }} °C</p>
    <button @click="fetchWeatherData()">Sprawdź pogodę</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      city: '',
      weatherData: {}
    }
  },
  methods: {
    async fetchWeatherData() {
      try {
        const apiKey = 'f061216668c5336449d17e06d1a06c8c'
        const response = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${apiKey}&lang=pl`)
        const data = await response.json()
        this.weatherData = {
          description: data.weather[0].description,
          temp: data.main.temp - 273.15
        }
      } catch (error) {
        console.error(error)
      }
    }
  }
}
</script>

<style>
  body{
    background-color: #87CEEB;
    letter-spacing: 0.2rem;
    font-size: 0.8em;
    margin: 0;
  }

  .container {
      width: 60%;
      padding-right: 15px;
      padding-left: 15px;
      margin: 0 auto;
      text-align: center;
  }

  h1{
    text-align: center;
    margin-top: 1.5rem;
  }

  .change-location{
    text-align: center;
    margin-top: 1.5rem;
    color: #6c757d;
}


  input{
    display: block;
    margin: 15px auto;
    width: 100%;
    height: 2.25rem;
    padding: 1.5rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #6c757d;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    box-sizing: border-box;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
  button {
    background-color: #cc5500;
    border: none;
    color: white;
    padding: 25px 25px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    border-radius: 20px;
    cursor: pointer;
  }

  p{
    padding: 10px;
    font-size: x-large;
    text-align: center;
  }

</style>