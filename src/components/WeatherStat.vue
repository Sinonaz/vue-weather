<template>
  <p class="stat">
    <span class="stat__name">Влажность</span>
    <span class="stat__value">90%</span>
  </p>
</template>

<script setup></script>

<style scoped>
  .stat {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
    font-size: 28px;
    line-height: 1;
    color: white;
    text-transform: uppercase;
  }

  .stat__name {
    font-weight: 700;
  }

  .stat__value {
    font-weight: 500;
  }
</style>
