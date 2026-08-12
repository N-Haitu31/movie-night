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
const selectedMovie = ref(null);
const favorites = ref([]);
const currentView = ref("films");

function toggleFavorite(movieId) {
  if (favorites.value.includes(movieId)) {
    favorites.value = favorites.value.filter((id) => id !== movieId);
  } else {
    favorites.value.push(movieId);
  }
}

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

const favoriteCount = computed(() => favorites.value.length);

const favoriteMovies = computed(() =>
  movies.value.filter((movie) => favorites.value.includes(movie.id))
);
</script>

<template>
    <div id="app" class="flex min-h-screen flex-col bg-slate-950 text-white">
      <AppHeader :favoriteCount="favoriteCount" @navigate="currentView = $event" />

    <main class="mx-auto w-full max-w-7xl flex-1 px-4 py-10 sm:px-6 lg:px-8">
      <TopSection v-model:search="search" v-model:category="selectedCategory" v-model:currentView="currentView" />

      <div v-if="isLoading" class="mt-16 flex flex-col items-center gap-3">
        <div
          class="h-30 w-30 animate-spin rounded-full border-4 border-slate-700 border-t-red-500"
        ></div>
        <p class="text-slate-100">Chargement des films...</p>
      </div>

      <InfoCard
        v-else-if="errorMessage"
        title="Impossible de charger les films"
        :message="errorMessage"
        button-label="Réessayer"
        @action="loadMovies"
      />

      <template v-else>
        <div v-if="currentView === 'films'" class="mt-8 grid grid-cols-1 gap-4 sm:grid-cols-2 lg:grid-cols-4">
          <MovieCard
            v-for="movie in filteredMovies"
            :key="movie.id"
            :movie="movie"
            :is-favorite="favorites.includes(movie.id)"
            @toggle-favorite="toggleFavorite"
            @display-details="
              selectedMovie = movies?.find((movie) => movie.id === $event) || null
            "
          />
        </div>
        
        <div v-else class="mt-8 grid grid-cols-1 gap-4 sm:grid-cols-2 lg:grid-cols-4">
          <template v-if="favoriteMovies.length > 0">
            <MovieCard
              v-for="movie in favoriteMovies"
              :key="movie.id"
              :movie="movie"
              :is-favorite="favorites.includes(movie.id)"
              @toggle-favorite="toggleFavorite"
              @display-details="
                selectedMovie = movies?.find((movie) => movie.id === $event) || null
              "
            />
          </template>
          <div v-else class="col-span-full flex flex-col items-center justify-center py-12">
            <p class="text-slate-300">Aucun favori pour le moment</p>
            <button
              class="mt-4 rounded-full bg-rose-500 px-4 py-2 text-sm font-semibold text-white transition hover:bg-rose-600"
              @click="currentView = 'films'"
            >
              Retour aux films
            </button>
          </div>
        </div>
      </template>

      <div
        v-if="selectedMovie"
        class="fixed inset-0 z-50 flex items-center justify-center bg-black/70 backdrop-blur-sm"
        @click.self="selectedMovie = null"
      >
        <MovieDetails :movie="selectedMovie" @close="selectedMovie = null" />
      </div>
    </main>

    <AppFooter />
  </div>
</template>
