<script setup>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import MovieCard from "./components/MovieCard.vue";
import MovieDetails from "./components/MovieDetails.vue";
</script>

<template>
  <div id="app" class="flex min-h-screen flex-col bg-slate-950 text-white">
    <AppHeader />
    <main class="mx-auto w-full max-w-7xl flex-1 px-4 py-10 sm:px-6 lg:px-8">
      <MovieCard />
      <MovieDetails />
    </main>
    <AppFooter />
  </div>
</template>
