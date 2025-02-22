<script setup lang="ts">
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import axios from "axios";
import moment from 'moment'

const apiUrl = import.meta.env.VITE_API_URL; 
const route = useRoute();
const post = ref(null);
const loading = ref(true);
const error = ref(null);

const fetchPost = async () => {
  try {
    const response = await axios.get(`${apiUrl}posts/${route.params.id}`);
    post.value = response.data.data;
  } catch (err) {
    error.value = "Failed to load the post. Please try again later.";
  } finally {
    loading.value = false;
  }
};


onMounted(fetchPost);
</script>

<template>
  <div class="container my-4">
    <!-- Back Button -->
    <router-link to="/" class="btn btn-outline-primary mb-3">
      ← Back to Posts
    </router-link>

    <!-- Loading Indicator -->
    <div v-if="loading" class="text-center">
      <div class="spinner-border text-primary" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>

    <!-- Error Message -->
    <div v-else-if="error" class="alert alert-danger text-center">
      {{ error }}
    </div>

    <!-- Blog Post Content -->
    <div v-else-if="post" class="card shadow-lg">
      <div class="card-body">
        <h1 class="card-title">{{ post.title }}</h1>
        <h6 class="text-muted">Date posted: {{moment(post.date_posted).format('MMMM Do YYYY, h:mm:ss a')}}</h6>
        <hr />
        <div class="card-text" v-html="post.content"></div>
      </div>
    </div>
  </div>
</template>
