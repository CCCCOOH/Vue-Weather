<template>
  <div class="flex flex-col flex-1 items-center">
    <!-- Banner -->
    <div
      v-if="route.query.preview"
      class="text-white p-4 bg-weather-secondary w-full text-center"
    >
      <p>
        You are currently previewing this city, click the "+" icon to start
        tracking this city.
      </p>
    </div>
    <!-- Weather Overview -->
    <div class="flex flex-col items-center text-white py-12">
      <h1 class="text-4xl mb-2">{{ weatherData.city }}</h1>
      <p class="text-sm mb-8">{{ weatherData.reporttime}}</p>
      <p class="text-8xl mb-8">{{ weatherData.temperature}}&deg;</p>
      <p class="capitalize">{{ weatherData.weather }}</p>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { useRoute } from "vue-router";
import { ref } from "vue";

const route = useRoute();
const apiKey = ref("51466edcbb25f717840d52b5bc19842e");

const getWeatherData = async () => {
  try {
    const weatherData = await axios.get(
      `https://restapi.amap.com/v3/weather/weatherInfo?key=${apiKey.value}&city=${route.query.adcode}`
    );
    return weatherData.data.lives[0];
  } catch (err) {
    console.log(err);
  }
};

const weatherData = await getWeatherData();
console.log(weatherData);
</script>
