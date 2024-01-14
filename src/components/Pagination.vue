<script setup>
const props = defineProps({
    pages: Number,
    currentPage: Number
});
const emit  = defineEmits(['update:currentPage']);

const changePage = (pageNumber) => {
    emit('update:currentPage', pageNumber);
}
</script>

<template>
    <nav>
        <ul class="pagination">
            <li class="page-item" v-if="currentPage !== 1">
                <span class="page-link" @click="changePage(currentPage - 1)">
                    <span>&laquo;</span>
                </span>
            </li>
            <li class="page-item" v-for="page in pages" :class="{ 'active': page === currentPage }">
                <span class="page-link" v-if="page <= 10" @click="changePage(page)">
                    {{ page }}
                </span>
            </li>
            <li class="page-item" v-if="currentPage !== pages">
                <span class="page-link" @click="changePage(currentPage + 1)">
                    <span>&raquo;</span>
                </span>
            </li>
        </ul>
    </nav>
</template>