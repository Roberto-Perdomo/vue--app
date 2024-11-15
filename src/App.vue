<template>
  <div id="app">
    <WeatherInfo />
  </div>
</template>

<script>
import WeatherInfo from './components/WeatherInfo.vue';

export default {
  components: {
    WeatherInfo
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
