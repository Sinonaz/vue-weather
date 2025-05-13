<template>
  <div class="info">
    <div class="info__header">
      <p class="info__day">
        {{ data ? new Date(data.date).toLocaleDateString('ru-Ru', { weekday: 'long' }) : '-' }}
      </p>
      <p class="info__date">
        {{ data ? new Date(data.date).toLocaleDateString('ru-Ru', { dateStyle: 'long' }) : '-' }}
      </p>
      <p class="info__location">{{ location ?? '-' }}</p>
    </div>

    <div class="info__footer">
      <IconSun v-if="data && data.day.condition.code <= 1003" width="95" height="95" />
      <IconCloud
        v-if="data && data.day.condition.code >= 1006 && data.day.condition.code < 1063"
        width="95"
        height="95"
      />
      <IconRain v-if="data && data.day.condition.code >= 1063" width="95" height="95" />

      <p class="info__temp">{{ data ? data.day.avgtemp_c : '-' }} °C</p>
      <p class="info__condition">{{ data ? data.day.condition.text : '-' }}</p>
    </div>
  </div>
</template>

<script setup>
  import IconCloud from './Icons/weather/IconCloud.vue'
  import IconRain from '@/components/Icons/weather/IconRain.vue'
  import IconSun from '@/components/Icons/weather/IconSun.vue'

  const { location, data } = defineProps({
    location: String,
    data: Object,
  })
</script>

<style scoped>
  .info {
    position: relative;
    z-index: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 100%;
    padding: 48px 32px;
    background: url('@/assets/bg.png') no-repeat center / cover;
    border-radius: 30px;
    color: white;
    overflow: hidden;
  }

  .info::before {
    content: '';
    position: absolute;
    z-index: -1;
    inset: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(
      152.19deg,
      rgba(136, 235, 239, 0.9) -0.04%,
      rgba(83, 91, 230, 0.9) 100%
    );
    opacity: 0.8;
  }

  .info__day {
    margin: 0 0 16px;
    font-weight: 700;
    font-size: 37px;
  }

  .info__date {
    margin: 0 0 10px;
    font-weight: 500;
    font-size: 22px;
  }

  .info__location {
    display: flex;
    align-items: center;
    gap: 8px;
    margin: 0;
    font-weight: 600;
    font-size: 20px;
  }

  .info__location::before {
    content: '';
    flex-shrink: 0;
    width: 27px;
    height: 27px;
    background: url('@/assets/location.svg') no-repeat center / contain;
  }

  .info__footer {
    display: flex;
    flex-direction: column;
    gap: 9px;
  }

  .info__temp {
    margin: 0 0 4px;
    font-weight: 700;
    font-size: 50px;
  }

  .info__condition {
    margin: 0;
    font-weight: 700;
    font-size: 30px;
  }
</style>
