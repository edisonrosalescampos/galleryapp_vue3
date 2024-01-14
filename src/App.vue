<script setup>
import { ref, watch, onMounted } from 'vue';
import axios from 'axios';
import SearchForm from './components/SearchForm.vue';
import ImageList from './components/ImageList.vue';
import Pagination from './components/Pagination.vue'

const totalImages   = ref(0);
const images        = ref([]);
const searchTerm    = ref("");
const isLoading     = ref(false);

const pages         = ref(10);
const currentPage   = ref(1);
const itemsPerPage  = 40;

const API_URL       = "https://pixabay.com/api/";
const API_KEY       = "24867302-6a5bcc62ddb787bd1b750a716";

const getImagesFromPixabayAPI = () => {
  document.getElementsByTagName('html')[0].scrollTo({ top: 0, behavior: "smooth" });

  isLoading.value = true;

  axios
    .get(API_URL, {
      params: { key: API_KEY, q: searchTerm.value.toLowerCase(), page: currentPage.value, per_page: itemsPerPage }
    })
    .then(({ data }) => {
      // console.log(data)

      totalImages.value = data.total;
      images.value      = data.hits;
      pages.value       = Math.ceil(data.totalHits / itemsPerPage);
    })
    .catch(error => {
      console.log(error);
    })
    .finally(() => {
      isLoading.value = false;
    });
}

watch(searchTerm, () => {  
  getImagesFromPixabayAPI();
});
watch(currentPage, () => {  
  getImagesFromPixabayAPI();
});

onMounted(() => {
  getImagesFromPixabayAPI();
});
</script>

<template>
  <div class="gallery container my-4">
    <h3 class="title">Gallery App</h3>

    <SearchForm v-model:searchTerm="searchTerm" />

    <p class="text-center mb-0" v-if="isLoading"><i class="fa fa-spinner fa-spin me-1"></i> loading, wait a moment please...</p>
    <p class="text-center mb-0" v-else-if="totalImages === 0">sorry, no results found</p>

    <ImageList :images="images" />

    <Pagination :pages="pages" v-model:currentPage="currentPage" v-if="totalImages > itemsPerPage" />    
  </div>
</template>