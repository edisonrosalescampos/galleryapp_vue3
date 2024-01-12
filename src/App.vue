<script setup>
import { onMounted, ref, watch } from 'vue';
import axios from 'axios';
import SearchForm from './components/SearchForm.vue';
import ImageList from './components/ImageList.vue';

const totalImages = ref(0);
const images      = ref([]);
const searchTerm  = ref("");
const isLoading   = ref(false);

const API_URL = "https://pixabay.com/api/";
const API_KEY = "24867302-6a5bcc62ddb787bd1b750a716";

const getImagesFromPixabayAPI = (search = "") => {
  images.value.length = 0;
  isLoading.value     = true;

  axios
    .get(API_URL, {
      params: { 
        key: API_KEY, 
        q: search.toLowerCase() 
      }
    })
    .then(({ data }) => {
      const { total, hits } = data;

      totalImages.value = total; 
      images.value      = hits;
    })
    .catch(error => {
      console.log(error);
    })
    .finally(() => {
      isLoading.value = false;
    });
}
const getSearchTerm = (text) => {
  searchTerm.value = text;
}

watch(searchTerm, (newSearchTerm, oldSearchTerm) => {  
  getImagesFromPixabayAPI(newSearchTerm);
});

onMounted(() => {
  getImagesFromPixabayAPI();
});
</script>

<template>
  <div class="gallery container my-4">
    <h2 class="title">
      Gallery App
    </h2>

    <SearchForm @search="getSearchTerm" />

    <p class="text-center mb-0" v-if="isLoading">
      <i class="fa fa-spinner fa-spin me-1"></i> loading, wait a moment please...
    </p>

    <p class="text-center mb-0" v-if="!isLoading && totalImages > 0">
      ({{ totalImages }}) results found
    </p>

    <ImageList :images="images" />
  </div>
</template>