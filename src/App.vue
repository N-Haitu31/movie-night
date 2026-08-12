<script setup>
import { ref, onMounted, computed } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import TopSection from "./components/TopSection.vue";
import MovieCard from "./components/MovieCard.vue";
import MovieDetails from "./components/MovieDetails.vue";
import InfoCard from "./components/InfoCard.vue";

const movies = ref([]);
const isLoading = ref(true);
const errorMessage = ref("");
const search = ref("");
const selectedCategory = ref("Tous");

async function loadMovies() {
  isLoading.value = true;
  errorMessage.value = "";

  try {
    await new Promise((resolve) => setTimeout(resolve, 2000));
    const response = await fetch("/data/movies.json");

    if (!response.ok) {
      throw new Error("Réponse invalide du serveur");
    }

    movies.value = await response.json();
  } catch (error) {
    errorMessage.value = "Une erreur est survenue pendant le chargement.";
  } finally {
    isLoading.value = false;
  }
}

onMounted(() => {
  loadMovies();
});

const filteredMovies = computed(() =>
  movies.value.filter((movie) => {
    const matchesCategory =
      selectedCategory.value === "Tous" ||
      movie.category === selectedCategory.value;
    const matchesSearch = movie.title
      .toLowerCase()
      .includes(search.value.toLowerCase());

    return matchesCategory && matchesSearch;
  }),
);
</script>

<template>
  <div id="app" class="flex min-h-screen flex-col bg-slate-950 text-white">
    <AppHeader />
    <main class="mx-auto w-full max-w-7xl flex-1 px-4 py-10 sm:px-6 lg:px-8">
      <TopSection v-model:search="search" v-model:category="selectedCategory" />

      <div v-if="isLoading" class="mt-16 flex flex-col items-center gap-3">
        <div class="h-30 w-30 animate-spin rounded-full border-4 border-slate-700 border-t-red-500"></div>
        <p class="text-slate-100">Chargement des films...</p>
      </div>

      <InfoCard
        v-else-if="errorMessage"
        title="Impossible de charger les films"
        :message="errorMessage"
        button-label="Réessayer"
        @action="loadMovies"
      />

      <div v-else class="mt-8 grid grid-cols-1 gap-4 sm:grid-cols-2 lg:grid-cols-4">
        <MovieCard
          v-for="movie in filteredMovies"
          :key="movie.id"
          :movie="movie"
          @toggle-favorite="console.log($event)"
        />
      </div>
    </main>
    <AppFooter />
  </div>
</template>
