<template>
    <div>
      <section class="container my-3">
        <div class="row">
          <div class="col-md-4" v-for="item in filteredPosts" :key="item.id">
            <div class="card rounded-top-4 m-2">
              <img :src="item.img" class="rounded-top-4" :alt="item.title">
              <div class="card-body">
                <h5 class="card-title">{{ item.title }}</h5>
                <p class="card-text">{{ item.short }}</p>
                <RouterLink :to="`details/${item.id}`" class="btn btn-primary">Read More..</RouterLink>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
</template>
  
<script setup>
import { RouterLink } from 'vue-router'
import { ref, toRefs, onMounted, computed, defineProps, watch } from 'vue';
import axios from 'axios';

const props = defineProps({
    selectedCategory: Number, 
});
const { selectedCategory } = toRefs(props);

const categoryId = ref(1);

const posts = ref([]);

const fetchPosts = async () => { 
    const response = await axios.get(`https://basic-blog.teamrabbil.com/api/post-list/${categoryId.value}`);
        posts.value = response.data;  

};


onMounted(() => {
    fetchPosts();
    watch(selectedCategory, () => {
        categoryId.value = selectedCategory.value;
        fetchPosts();
    });
});


const filteredPosts = computed(() => {
    return posts.value.filter(post => post.category_id === categoryId.value);
});
</script>