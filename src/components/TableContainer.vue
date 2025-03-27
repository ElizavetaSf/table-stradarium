<script setup>
import { ref, onMounted, computed } from 'vue'
import SearchInput from './SearchInput.vue'
import Table from './Table.vue'

const LoadStatus = {
	LOADING: 'loading',
	ERROR: 'error',
	SUCCESS: 'success',
}
const status = ref(LoadStatus.LOADING)
const searchQuery = ref('')
const posts = ref([])

const updateQuery = newQuery => {
	searchQuery.value = newQuery
}

async function fetchPosts() {
	status.value = LoadStatus.LOADING
	try {
		const response = await fetch('https://jsonplaceholder.typicode.com/posts')
		if (!response.ok) {
			throw new Error(`Ошибка: ${response.status}`)
		}
		const data = await response.json()
		posts.value = data
		status.value = LoadStatus.SUCCESS
	} catch (error) {
		console.error('Ошибка при загрузке постов:', error)
		status.value = LoadStatus.ERROR
	}
}

onMounted(async () => {
	await fetchPosts()
})

const filteredPosts = computed(() => {
	if (!searchQuery.value) {
		return posts.value
	}
	return posts.value.filter(post =>
		post.title.toLowerCase().includes(searchQuery.value.toLowerCase())
	)
})
</script>

<template>
	<div v-if="status === 'loading'">Загрузка...</div>
	<div v-else-if="status === 'error'">Ошибка загрузки :(</div>
	<div v-else>
		<SearchInput @update:query="updateQuery" />
		<Table :filteredPosts="filteredPosts" />
	</div>
</template>

<style scoped></style>
