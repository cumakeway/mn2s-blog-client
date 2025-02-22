<script setup lang="ts">
import { ref, onMounted } from "vue";
import axios from "axios";
import moment from 'moment'

const apiUrl = import.meta.env.VITE_API_URL; 
const posts = ref([]);
const loading = ref(true);

const fetchPosts = async () => {
  try {
    const response = await axios.get(`${apiUrl}posts`);
    console.log(response);
    posts.value = response.data.data; 
  } catch (error) {
    console.error("Error fetching posts:", error);
  } finally {
    loading.value = false;
  }
};

onMounted(fetchPosts);

</script>

<template>
<div class="container my-4">
    <h1 class="mb-4">Blog Posts</h1>

    <!-- Loading Indicator -->
    <div v-if="loading" class="text-center">
      <div class="spinner-border text-primary" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>

    <!-- Posts Content -->
    <div v-else>
      <div v-if="posts.length === 0" class="alert alert-info text-center">
        No posts available.
      </div>

      <div v-for="post in posts" :key="post.id" class="row mb-3">
          <div class="card h-100 shadow-sm">
            <div class="card-body">
              <h5 class="card-title">{{ post.title }}</h5>
              <h6 class="card-subtitle mb-2 text-muted">Date posted: {{moment(post.date_posted).format('MMMM Do YYYY, h:mm:ss a')}} {{  }}</h6>
              <div v-html="post.excerpt" class="card-text"></div>
              <a href="#" class="btn btn-primary">Read More...</a>
            </div>
          </div>
        </div>

    
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 800px;
}
</style>
