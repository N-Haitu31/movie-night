<script setup>
const categories = [
  "Tous",
  "Action",
  "Comédie",
  "Science-fiction",
  "Animation",
];
const selectedCategory = defineModel("category");
const search = defineModel("search");
const currentView = defineModel("currentView");
</script>

<template>
  <section
    class="rounded-2xl border border-slate-800 bg-slate-950 px-6 py-10 sm:px-10"
  >
    <div v-if="currentView === 'favorites'">
      <p class="text-sm font-bold uppercase tracking-[0.2em] text-rose-400">
        Ma sélection
      </p>
      <h1 class="mt-3 text-4xl font-black tracking-tight sm:text-5xl">
        Mes favoris
      </h1>
      <p class="mt-4 text-slate-400">
        Retrouvez ici les films que vous avez gardés pour plus tard.
      </p>
    </div>
    <div v-else>
      <p class="text-xs font-bold tracking-[0.2em] text-rose-500 uppercase">
        Votre soirée commence ici
      </p>

      <h1
        class="mt-3 text-4xl font-extrabold tracking-tight text-white sm:text-5xl"
      >
        Quel film pour ce soir ?
      </h1>

      <p class="mt-3 text-sm text-slate-400">
        Recherchez un titre, filtrez par catégorie et gardez vos favoris.
      </p>
    </div>

    <div v-if="currentView === 'films'" class="mt-8 flex flex-col gap-3 sm:flex-row sm:items-center">
      <input
        v-model="search"
        type="search"
        placeholder="Rechercher un film..."
        aria-label="Rechercher un film"
        class="w-full flex-1 rounded-2xl border border-slate-800 bg-slate-900 px-4 py-3 text-white transition outline-none placeholder:text-slate-500 focus:border-rose-500"
      />

      <div class="flex flex-wrap gap-2">
        <button
          v-for="category in categories"
          :key="category"
          type="button"
          @click="selectedCategory = category"
          class="rounded-full px-4 py-2 text-sm font-semibold transition"
          :class="
            category === selectedCategory
              ? 'bg-rose-500 text-white'
              : 'bg-slate-900 text-slate-300 hover:bg-slate-800'
          "
        >
          {{ category }}
        </button>
      </div>
    </div>
  </section>
</template>
