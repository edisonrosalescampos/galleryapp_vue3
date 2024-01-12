<script setup>
import { ref } from 'vue';

const emit = defineEmits(['search']);

const txtSearchTerm = ref("");

const submitForm = () => {
  if (txtSearchTerm.value.trim() !== "") 
  {
    emit('search', txtSearchTerm.value);
  }
  else
  {
    alert("Search box cannot be blank!")
  }

  txtSearchTerm.value = ""
}
</script>

<template>
  <form @submit.prevent="submitForm">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div class="search-container">
          <input type="text" class="form-control" placeholder="Type a search..." maxlength="100" v-model="txtSearchTerm">
          <button class="addon">
            <i class="fa fa-search"></i>
          </button>
        </div>
      </div>
    </div>
  </form>
</template>