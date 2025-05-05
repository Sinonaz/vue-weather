<script setup>
	import Button from './components/Button.vue'

	const date = new Date().toLocaleString()
</script>

<template>
	<h1>{{ date }}</h1>
	<Button text="Button" />
</template>

<style scoped></style>
