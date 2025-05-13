<template>
  <div class="right-panel">
    <div class="right-panel__stats">
      <WeatherStat v-for="stat in statsData" :key="stat.label" v-bind="stat" />
    </div>

    <div v-if="forecast.forecast" class="right-panel__days">
      <DayCard
        v-for="(day, index) in forecast.forecast.forecastday"
        :key="day.date"
        :date="new Date(day.date)"
        :temp="day.day.avgtemp_c"
        :weather-code="day.day.condition.code"
        :is-active="activeIndex === index"
        @click="emit('update:active-index', index)"
      />
    </div>

    <CitySelect />

    <AppError v-if="error" :error="errorDisplay" class="right-panel__error" />
  </div>
</template>

<script setup>
  import { computed } from 'vue'
  import AppError from './AppError.vue'
  import CitySelect from './CitySelect.vue'
  import DayCard from './DayCard.vue'
  import WeatherStat from './WeatherStat.vue'
  import { errorMap } from '@/constants.js'

  const { error, forecast, activeIndex } = defineProps({
    error: Object,
    forecast: Object,
    activeIndex: Number,
  })

  const emit = defineEmits(['update:active-index'])

  const statsData = computed(() => {
    return [
      {
        label: 'Влажность',
        value:
          forecast.forecast && !error
            ? `${forecast.forecast.forecastday[activeIndex].day.avghumidity} %`
            : '-',
      },
      {
        label: 'Вероятность дождя',
        value:
          forecast.forecast && !error
            ? `${forecast.forecast.forecastday[activeIndex].day.daily_chance_of_rain} %`
            : '-',
      },
      {
        label: 'Ветер',
        value:
          forecast.forecast && !error
            ? `${forecast.forecast.forecastday[activeIndex].day.maxwind_kph} км/ч`
            : '-',
      },
    ]
  })
  const errorDisplay = computed(() => errorMap.get(error.error?.code))
</script>

<style scoped>
  .right-panel {
    justify-self: end;
    grid-column: 2;
    grid-row: 1;
    display: grid;
    gap: 70px;
    width: 100%;
    position: relative;
    padding: 60px 50px;
  }

  .right-panel__error {
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

  .right-panel__days {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 2px;
  }

  .right-panel__stats {
    display: flex;
    flex-direction: column;
    gap: 17px;
  }
</style>
