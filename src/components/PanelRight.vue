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

    <CitySelect @update:city="(city) => emit('update:city', city)" />

    <AppError v-if="error" :error="errorDisplay" class="right-panel__error" />
  </div>
</template>

<script setup>
  import { computed } from 'vue'
  import AppError from './AppError.vue'
  import CitySelect from './CitySelect.vue'
  import DayCard from './DayCard.vue'
  import WeatherStat from './WeatherStat.vue'

  const { error, forecast, activeIndex } = defineProps({
    error: Object,
    forecast: Object,
    activeIndex: Number,
  })

  const emit = defineEmits(['update:city', 'update:active-index'])

  const errorMap = new Map([[1006, 'Город не найден']])

  const statsData = computed(() => {
    return [
      {
        label: 'Влажность',
        value: forecast.current && !error ? `${forecast.current.humidity} %` : '-',
      },
      {
        label: 'Облачность',
        value: forecast.current && !error ? `${forecast.current.cloud} %` : '-',
      },
      {
        label: 'Ветер',
        value: forecast.current && !error ? `${forecast.current.wind_kph} км/ч` : '-',
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
