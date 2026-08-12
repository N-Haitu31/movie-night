<script setup>
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import MovieCard from './components/MovieCard.vue'
import MovieDetails from './components/MovieDetails.vue'
</script>

<template>
  <div id="app">
    <AppHeader />
    <main>
      <MovieCard />
      <MovieDetails />
    </main>
    <AppFooter />
  </div>
</template>
