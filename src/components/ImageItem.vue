<script setup>
import { ref } from 'vue';
import preloader from './../assets/preloader-dark.gif'

const imageURL = ref(preloader); 

const props = defineProps({
    image: Object
});

setTimeout(() => imageURL.value = props.image.webformatURL, 300);
</script>

<template>
    <div class="photos-item">
        <div class="card">
            <div class="card-img-container">
                <img :src="imageURL" class="card-img-top" alt="...">
            </div>
            <div class="card-body">
                <p class="card-text text-truncate">
                    {{ image.tags }}
                </p>
            </div>
            <div class="card-footer">
                <span>
                    <i class="fas fa-thumbs-up"></i> {{ image.likes }}
                </span>

                <span>
                    <i class="fas fa-comments"></i> {{ image.comments }}
                </span>
            </div>
        </div>
    </div>
</template>