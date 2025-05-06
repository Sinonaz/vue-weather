<template>
  <div class="city-select">
    <AppButton class="city-select__change">
      <IconLocation />
      Изменить город
    </AppButton>

    <div class="city-select__label">
      <input type="text" name="city-select" placeholder="Введите город" />
      <AppButton>Сохранить</AppButton>
    </div>
  </div>
</template>

<script setup>
  import AppButton from './AppButton.vue'
  import IconLocation from './Icons/IconLocation.vue'
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

  input {
    width: auto;
    padding: 15px;
    color: white;
    font-size: 18px;
    font-family: var(--font);
    background: var(--gray);
    border: none;
    border-radius: 10px;
    box-shadow: 1px 2px 4px 0px #222831;
    outline: none;

    &::placeholder {
      color: #3f4958;
    }
  }
</style>
