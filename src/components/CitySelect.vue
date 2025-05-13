<template>
  <div class="city-select">
    <AppButton v-if="!isEdited" class="city-select__change" @click="isEdited = true">
      <IconLocation />
      Изменить город
    </AppButton>

    <div v-else class="city-select__label">
      <AppInput
        v-model="inputValue"
        @keyup.enter="selectCity()"
        v-focus
        type="text"
        name="city-select"
        placeholder="Введите город"
      />
      <AppButton @click="selectCity()">Сохранить</AppButton>
    </div>
  </div>
</template>

<script setup>
  import { inject, ref } from 'vue'
  import AppButton from './AppButton.vue'
  import IconLocation from './Icons/IconLocation.vue'
  import AppInput from './AppInput.vue'

  const city = inject('city')

  const isEdited = ref(false)
  const inputValue = ref(city.value)

  function selectCity() {
    city.value = inputValue.value
    isEdited.value = false
  }
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
