<script setup>
import { ref } from 'vue';

const emit = defineEmits(['update:searchTerm']);

const txtSearchTerm = ref("");

const submitForm = () => {
  emit('update:searchTerm', txtSearchTerm.value);
}
</script>

<template>
  <form @submit.prevent="submitForm">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div class="search-container">
          <input type="text" class="form-control" placeholder="Type a search or empty for all results..." maxlength="100" v-model="txtSearchTerm">
          <button class="addon">
            <i class="fa fa-search"></i>
          </button>
        </div>
      </div>
    </div>
  </form>
</template>