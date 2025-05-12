<template>
  <button class="day-card" :class="{ 'day-card--active': isActive }">
    <IconSun v-if="weatherCode === 1000" :color="isActive ? 'black' : 'white'" />
    <IconCloud v-if="weatherCode === 1189" :color="isActive ? 'black' : 'white'" />
    <IconRain v-if="weatherCode === 1063" :color="isActive ? 'black' : 'white'" />

    <p class="day-card__day-name">{{ date.toLocaleDateString('ru-RU', { weekday: 'short' }) }}</p>
    <p class="day-card__stat">{{ temp }} ℃</p>
  </button>
</template>

<script setup>
  import IconCloud from './Icons/weather/IconCloud.vue'
  import IconRain from './Icons/weather/IconRain.vue'
  import IconSun from './Icons/weather/IconSun.vue'

  defineProps({
    date: Date,
    temp: Number,
    weatherCode: Number,
    isActive: Boolean,
  })
</script>

<style scoped>
  .day-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 15px;
    padding: 15px 25px;
    background: var(--gray);
    color: white;
    border-radius: 10px;
    border: none;
    font-size: 20px;
    box-shadow: 1px 2px 4px 0px #222831;

    &:not(.day-card--active) {
      cursor: pointer;

      &:hover {
        background: #3a434f;
      }
    }
  }

  .day-card--active {
    color: black;
    background: white;
  }

  .day-card__day-name {
    margin: 0;
  }

  .day-card__stat {
    margin: 0;
    font-weight: 700;
    white-space: nowrap;
  }
</style>
