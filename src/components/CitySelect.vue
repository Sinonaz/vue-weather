<template>
  <div class="city-select">
    <AppButton v-if="!isEdited" class="city-select__change" @click="isEdited = true">
      <IconLocation />
      Изменить город
    </AppButton>

    <div v-else class="city-select__label">
      <AppInput v-model="city" type="text" name="city-select" placeholder="Введите город" />
      <AppButton @click="selectCity()">Сохранить</AppButton>
    </div>
  </div>
</template>

<script setup>
  import { onMounted, ref } from 'vue'
  import AppButton from './AppButton.vue'
  import IconLocation from './Icons/IconLocation.vue'
  import AppInput from './AppInput.vue'

  const emit = defineEmits(['update:city'])

  const city = ref('Калининград')
  const isEdited = ref(false)

  function selectCity() {
    emit('update:city', city.value)
    isEdited.value = false
  }

  onMounted(() => {
    emit('update:city', city.value)
  })
</script>

<style scoped>
  .city-select {
    display: grid;
  }

  .city-select__change {
    justify-content: center;
  }

  .city-select__label {
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 20px;
  }
</style>
