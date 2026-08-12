<script setup>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import TopSection from "./components/TopSection.vue";
import MovieCard from "./components/MovieCard.vue";
import MovieDetails from "./components/MovieDetails.vue";
import { computed, ref } from "vue";

const search = ref("");
const selectedCategory = ref("Tous");
const testMovies = [
  {
    id: 1,
    title: "Interstellar",
    category: "Science-fiction",
    rating: 8.7,
    year: 2014,
    duration: "2h49",
    favorite: false,
    image: "https://image.tmdb.org/t/p/w500/gEU2QniE6E77NI6lCU6MxlNBvIx.jpg",
    description: "Une équipe d'explorateurs voyage dans l'espace pour trouver une nouvelle chance pour l'humanité.",
  },
  {
    id: 2,
    title: "The Batman",
    category: "Action",
    rating: 7.8,
    year: 2022,
    duration: "2h56",
    favorite: false,
    image: "https://image.tmdb.org/t/p/w500/74xTEgt7R36Fpooo50r9T25onhq.jpg",
    description: "Batman enquête sur une série de crimes qui touche les élites de Gotham.",
  },
  {
    id: 3,
    title: "Ratatouille",
    category: "Animation",
    rating: 8.1,
    year: 2007,
    duration: "1h51",
    favorite: false,
    image: "https://image.tmdb.org/t/p/w500/t3vaWRPSf6WjDSamIkKDs1iQWna.jpg",
    description: "Un jeune rat passionné de cuisine rêve de devenir un grand chef à Paris.",
  },
  {
    id: 4,
    title: "Dune",
    category: "Science-fiction",
    rating: 8.0,
    year: 2021,
    duration: "2h35",
    favorite: false,
    image: "https://image.tmdb.org/t/p/w500/d5NXSklXo0qyIYkgV94XAgMIckC.jpg",
    description: "Paul Atreides rejoint la planète Arrakis et se retrouve au cœur d'un conflit gigantesque.",
  },
];

const filteredMovies = computed(() =>
  testMovies.filter((movie) => {
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
      <div class="mt-8 grid grid-cols-1 gap-4 sm:grid-cols-2 lg:grid-cols-4">
        <MovieCard
          v-for="movie in filteredMovies"
          :key="movie.id"
          :movie="movie"
        />
      </div>
    </main>
    <AppFooter />
  </div>
</template>
