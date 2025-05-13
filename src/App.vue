<script setup>
  import { ref } from 'vue'
  import InfoPanel from './components/InfoPanel.vue'
  import PanelRight from './components/PanelRight.vue'

  const API_ENDPOINT = 'http://api.weatherapi.com/v1/'
  const API_KEY = '6346860df8e747d2b20173736250705'

  const forecast = ref({})
  const error = ref()
  const activeIndex = ref(0)

  async function fetchForecast(city) {
    const params = new URLSearchParams({
      q: city,
      lang: 'ru',
      key: API_KEY,
      days: 4,
    }).toString()
    const response = await fetch(`${API_ENDPOINT}forecast.json?${params}`)

    if (response.status !== 200) {
      return (error.value = await response.json())
    }

    error.value = null
    forecast.value = await response.json()
  }
</script>

<template>
  <main class="main">
    <div class="weather">
      <InfoPanel class="weather__left" />

      <PanelRight
        :error
        :forecast
        :active-index="activeIndex"
        @update:city="(city) => fetchForecast(city)"
        @update:active-index="(i) => (activeIndex = i)"
      />
    </div>
  </main>
</template>

<style scoped>
  .main {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 50px;
  }

  .weather {
    display: flex;
    width: 100%;
    max-width: 942px;
    background: var(--dark-gray);
    border-radius: 25px;
  }

  .weather__left {
    margin: -25px 0;
  }
</style>
