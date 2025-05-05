<script setup>
import AppButton from './components/AppButton.vue'
import WeatherStat from './components/WeatherStat.vue'
</script>

<template>
  <main class="main">
    <div class="weather">
      <div class="weather__left"></div>

      <div class="weather__right">
        <div class="weather__stats">
          <WeatherStat />
        </div>

        <AppButton> Изменить город </AppButton>
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
