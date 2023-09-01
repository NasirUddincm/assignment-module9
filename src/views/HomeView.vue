<script setup>
import { ref } from 'vue';
import NavBar from '@/components/partials/NavBar.vue'
import FooterComponent from '@/components/partials/FooterComponent.vue'
import MainContent from '@/components/MainContent.vue'

const selectedCategory = ref(null);

const handleCategorySelected = (categoryId) => {
  selectedCategory.value = categoryId;
  console.log('selectedCategory in HomeViews:', selectedCategory.value);
};


</script>

<template>
  <div>
    <NavBar @categorySelected="handleCategorySelected" />
    <MainContent :selectedCategory="selectedCategory" />
    <FooterComponent/>

  </div>
</template>



