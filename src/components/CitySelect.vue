<template>
  <div class="city-select">
    <AppButton v-if="!isEdited" class="city-select__change" @click="edit(true)">
      <IconLocation />
      Изменить город
    </AppButton>

    <div v-else class="city-select__label">
      <AppInput type="text" name="city-select" placeholder="Введите город" />
      <AppButton @click="edit(false)">Сохранить</AppButton>
    </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue'
  import AppButton from './AppButton.vue'
  import IconLocation from './Icons/IconLocation.vue'
  import AppInput from './AppInput.vue'

  const isEdited = ref(false)

  function edit(isEdit) {
    isEdited.value = isEdit
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
