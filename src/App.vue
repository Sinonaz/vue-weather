<template>
  <h1>{{ date }}</h1>
</template>

<script setup>
const date = new Date().toLocaleString()
</script>

<style scoped></style>
