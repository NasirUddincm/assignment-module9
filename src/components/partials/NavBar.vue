<script setup>
import { RouterLink } from 'vue-router'
import { ref, onMounted, defineEmits } from 'vue';
import axios from 'axios';

const emits = defineEmits([]);

const categories = ref([]);

const fetchCategories = async () => {
  const response = await axios.get('https://basic-blog.teamrabbil.com/api/post-categories');
  categories.value = response.data;
};

onMounted(() => {
  fetchCategories();
});


const selectCategory = (categoryId) => {
  console.log('Selected Category:', categoryId);
  emits('categorySelected', categoryId);
};
</script>
<template>
    <div>
        <nav class="navbar shadow navbar-expand-lg bg-body-tertiary">
        <div class="container-fluid">
          <a class="navbar-brand" href="#">My Blog</a>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <RouterLink class="nav-link active" aria-current="page" to="/" @click="selectCategory(1)">হোম</RouterLink>
              </li>
              <li class="nav-item" v-for="category in categories" :key="category.id">
                <button class="nav-link" 
                  @click="selectCategory(category.id)">
                  {{ category.name }}
                </button>
              </li>
                           
            </ul>
            
          </div>
        </div>
    </nav> 
    </div>
</template>


