<template>
  <p class="stat">
    <span class="stat__name">{{ label }}</span>
    <span class="stat__value">{{ value }}</span>
  </p>
</template>

<script setup>
  defineProps({
    label: String,
    value: String,
  })
</script>

<style scoped>
  .stat {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
    margin: 0;
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
