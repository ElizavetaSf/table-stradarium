<script setup>
import { computed } from 'vue';
import DataTable from 'primevue/datatable';
import Column from 'primevue/column';
const props = defineProps({ filteredPosts: Array, })
const posts = computed(() => props.filteredPosts);

</script>

<template>
	<DataTable
		class="custom-table"
		:value="posts"
		paginator
		:rows="25"
		tableStyle="min-width: 50rem"
		responsive-layout="scroll"
    scrollable
    scrollHeight="80vh"
		showGridlines
	>
		<Column class="title-column" field="title" header="Заголовок" style="width: 40%"></Column>
		<Column field="body" header="Текст поста" style="width: 60%"></Column>
	</DataTable>
</template>

<style>

.custom-table .p-datatable-thead {
  --p-datatable-header-cell-background: rgba(255, 88, 65, 0.8);
}
.custom-table .p-datatable-thead > tr > th {
	padding: 12px;
}

.custom-table .p-datatable-column-title, .custom-table .title-column {
	font-weight: 700;
	text-transform: uppercase;
}
.custom-table .p-datatable-tbody > tr > td {
	padding: 10px;
}

.custom-table .p-datatable-paginator-bottom {
	margin-top: 10px;
	border: none;
}

.custom-table .p-paginator {
	--p-paginator-gap: 1em;
	padding: 12px;
}
.custom-table .p-paginator .p-paginator-page {
	font-size: 18px;
}
</style>
