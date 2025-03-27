<script setup>
import { ref } from 'vue'

const emit = defineEmits(['update:query'])
const localQuery = ref('')

const onInput = e => {
	localQuery.value = e.target.value
	emit('update:query', localQuery.value)
}
</script>

<template>
		<input
			type="text"
			:value="localQuery"
			@input="onInput"
			placeholder="Поиск по заголовку..."
			class="search-input"
		/>
</template>

<style>
.search-input {
	margin-bottom: 15px;
	padding: 8px;
	width: 39.5%;
	border: none;
}
</style>
