<template>
  <div>
    {{ error }}
  </div>
</template>

<script setup>
const props = defineProps({
  error: String
})
</script>
