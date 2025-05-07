<script setup>
  import { ref } from 'vue'
  import CitySelect from './components/CitySelect.vue'
  import WeatherStat from './components/WeatherStat.vue'

  const API_ENDPOINT = 'http://api.weatherapi.com/v1/'
  const API_KEY = '6346860df8e747d2b20173736250705'

  const cityStats = ref([
    {
      label: 'Влажность',
      value: '90%',
    },
    {
      label: 'Осадки',
      value: '0%',
    },
    {
      label: 'Ветер',
      value: '3 м/ч',
    },
  ])

  async function fetchForecast(city) {
    const params = new URLSearchParams({
      q: city,
      lang: 'ru',
      key: API_KEY,
      days: 3,
    }).toString()
    const response = await fetch(`${API_ENDPOINT}forecast.json?${params}`)
    const data = await response.json()
    console.log(data)
  }
</script>

<template>
  <main class="main">
    <div class="weather">
      <div class="weather__left"></div>

      <div class="weather__right">
        <div class="weather__stats">
          <WeatherStat v-for="stat in cityStats" :key="stat.label" v-bind="stat" />
        </div>

        <CitySelect @update:city="fetchForecast" />
      </div>
    </div>
  </main>
</template>

<style scoped>
  .main {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .weather {
    display: grid;
    grid-template-columns: auto 1fr;
    width: 100%;
    max-width: 942px;
    padding: 60px 50px;
    background: var(--dark-gray);
    border-radius: 25px;
  }

  .weather__right {
    max-width: 415px;
  }
</style>
