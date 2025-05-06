<template>
  <input />
</template>

<script setup></script>

<style>
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
