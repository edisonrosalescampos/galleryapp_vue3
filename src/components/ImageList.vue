<script setup>
import ImageItem from './ImageItem.vue'

defineProps({
    images: Array
});
</script>

<template>
    <div class="images">
        <ImageItem v-for="image in images" :image="image" :key="image.id" />
    </div>
</template>