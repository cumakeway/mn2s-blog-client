<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>


<template>
  <div class="container my-4">
    <!-- Navigation Bar -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
      <div class="container">
        <router-link class="navbar-brand" to="/">MN2S Blog Test</router-link>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <router-link class="nav-link" to="/">Posts</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Main Content -->
    <div class="flex-grow-1 container py-4">
      <RouterView />
    </div>

    <!-- Footer -->
    <footer class="bg-primary text-white text-center py-3">
      <div class="container">
        <p class="mb-0">&copy; 2025 MN2S Blog Test. All rights reserved.</p>
      </div>
    </footer>

  </div>
</template>


<style>
/* Additional global styles if needed */
</style>

