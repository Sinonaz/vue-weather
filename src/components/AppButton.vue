<template>
  <button type="button" class="button">
    <slot />
  </button>
</template>

<script setup></script>

<style scoped>
.button {
  padding: 14px;
  background: var(--gradient);
  border: none;
  color: var(--white);
  font-weight: 600;
  font-size: 20px;
  border-radius: 10px;
  font-family: var(--font-primary);
  cursor: pointer;
  transition: background 0.2s;

  &:hover,
  &:focus {
    background: var(--gradient-hover);
  }
}
</style>
