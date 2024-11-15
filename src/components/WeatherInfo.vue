<template>
    <div class="weather-info">
      <h1>Weather Information</h1>
      
      <!-- Campo de entrada para la ciudad -->
      <input
        type="text"
        v-model="city"
        placeholder="Enter city name"
        @keyup.enter="fetchWeather"
      />
      <button @click="fetchWeather">Get Weather</button>
  
      <!-- Mostrar los datos del clima si están disponibles -->
      <div v-if="weatherData" class="weather-details">
        <h2>Weather in {{ weatherData.city }}</h2>
        <p><strong>Temperature:</strong> {{ weatherData.temperature }}°C</p>
        <p><strong>Humidity:</strong> {{ weatherData.humidity }}%</p>
        <p><strong>Conditions:</strong> {{ weatherData.description }}</p>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: "WeatherInfo",  // Nombre actualizado del componente
    data() {
      return {
        city: '',        // Nombre de la ciudad ingresada por el usuario
        weatherData: null // Datos del clima recibidos del backend
      };
    },
    methods: {
      // Método para obtener los datos del clima desde el backend
      fetchWeather() {
        if (!this.city) {
          alert("Please enter a city name.");
          return;
        }
  
        // Realiza la solicitud HTTP al backend
        axios
          .get(`http://localhost:8081/api/weather?city=${this.city}`)
          .then((response) => {
            this.weatherData = response.data; // Guarda los datos de clima recibidos
          })
          .catch((error) => {
            console.error("Error fetching weather data:", error);
            alert("Could not fetch weather data. Please try again.");
          });
      }
    }
  };
  </script>
  
  <style scoped>
  .weather-info {
    text-align: center;
    font-family: Arial, sans-serif;
  }
  
  input {
    padding: 10px;
    font-size: 16px;
    margin-right: 10px;
  }
  
  button {
    padding: 10px 15px;
    font-size: 16px;
    cursor: pointer;
  }
  
  .weather-details {
    margin-top: 20px;
    text-align: left;
    display: inline-block;
  }
  
  .weather-details h2 {
    margin: 10px 0;
  }
  
  .weather-details p {
    margin: 5px 0;
  }
  </style>
  