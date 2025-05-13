<script setup>
  import { computed, ref } from 'vue'
  import CitySelect from './components/CitySelect.vue'
  import WeatherStat from './components/WeatherStat.vue'
  import AppError from './components/AppError.vue'
  import DayCard from './components/DayCard.vue'
  import InfoPanel from './components/InfoPanel.vue'

  const API_ENDPOINT = 'http://api.weatherapi.com/v1/'
  const API_KEY = '6346860df8e747d2b20173736250705'
  const errorMap = new Map([[1006, 'Город не найден']])

  const forecast = ref({})
  const error = ref()
  const activeIndex = ref(0)
  const statsModified = computed(() => {
    return [
      {
        label: 'Влажность',
        value:
          forecast.value.current && !error.value ? `${forecast.value.current.humidity} %` : '-',
      },
      {
        label: 'Облачность',
        value: forecast.value.current && !error.value ? `${forecast.value.current.cloud} %` : '-',
      },
      {
        label: 'Ветер',
        value:
          forecast.value.current && !error.value ? `${forecast.value.current.wind_kph} км/ч` : '-',
      },
    ]
  })
  const errorDisplay = computed(() => errorMap.get(error.value?.error?.code))

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

      <div class="weather__right">
        <div class="weather__stats">
          <WeatherStat v-for="stat in statsModified" :key="stat.label" v-bind="stat" />
        </div>

        <div v-if="forecast.forecast" class="weather__days">
          <DayCard
            v-for="(day, index) in forecast.forecast.forecastday"
            :key="day.date"
            :date="new Date(day.date)"
            :temp="day.day.avgtemp_c"
            :weather-code="day.day.condition.code"
            :is-active="activeIndex === index"
            @click="activeIndex = index"
          />
        </div>

        <CitySelect @update:city="fetchForecast" />
      </div>

      <AppError v-if="error" :error="errorDisplay" class="weather__error" />
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

  .weather__right {
    justify-self: end;
    grid-column: 2;
    grid-row: 1;
    display: grid;
    gap: 70px;
    width: 100%;
    position: relative;
    padding: 60px 50px;
  }

  .weather__error {
    grid-column: 2;
    grid-row: 1;
    height: fit-content;
    padding: 15px 50px;
    background-color: var(--gray);
    border-radius: 0 0 25px 25px;
    font-size: 18px;
    line-height: 1.1;
    text-align: center;
    box-shadow: 1px 2px 4px 0px #222831;
  }

  .weather__days {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 2px;
  }

  .weather__stats {
    display: flex;
    flex-direction: column;
    gap: 17px;
  }
</style>
