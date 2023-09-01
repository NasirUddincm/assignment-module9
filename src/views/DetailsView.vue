<script setup>
import {ref, onMounted} from 'vue'
import axios from 'axios'
import { useRoute, RouterLink } from 'vue-router';
import NavBar from '@/components/partials/NavBar.vue';
import FooterComponent from '@/components/partials/FooterComponent.vue'
    const detailsData = ref({})
    const route = useRoute(); 
    
    function details() {
        const id = route.params.id
        axios.get(`https://basic-blog.teamrabbil.com/api/post-details/${id}`)
            .then(response => {
                detailsData.value = response.data.postDetails;
            })
            .catch(error => {
            console.error('Error fetching customers:', error);
            });
    }

    onMounted(() => {
        details();
    });

</script>
<template>
    <div>
        <NavBar/>

        <section class="container mt-4">
            <div class="text-center">
                <RouterLink class="btn btn-dark" to="/">Back</RouterLink>
            </div>
            <div class="card rounded-top-4" v-if="detailsData != null">
                <img :src="detailsData.img" class="rounded-top-4" :alt="detailsData.title">
                <div class="card-body">
                <h3 class="card-title">{{detailsData.title}}</h3>
                <p class="card-text text-justify" 
                    style="text-align: justify;">
                    {{ detailsData.content }}
                </p>
                
                </div>
            </div> 
            <div class="card" v-else>
                <h4 class="text-center p-5">Data not found</h4>
            </div>
        </section>

        <FooterComponent/>
    </div>
</template>