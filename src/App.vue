<script setup>
import Button from './components/Button.vue'
</script>

<template>
  <main class="main">
    <div class="weather">
      <div class="weather__left"></div>

      <div class="weather__right">
        <Button> Изменить город </Button>
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
  grid-template-columns: 1fr auto;
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
