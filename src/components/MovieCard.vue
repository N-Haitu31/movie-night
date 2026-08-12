<script setup>
defineProps(['movie'])
</script>

<template>
  <div class="bg-slate-900 rounded-xl overflow-hidden shadow-lg hover:scale-[1.02] transition-transform duration-200">
    <div class="relative">
      <img
        :src="movie.image"
        :alt="movie.title"
        class="w-full h-64 object-cover"
      />
      <button
        class="absolute top-2 right-2 flex items-center justify-center w-8 h-8 rounded-full bg-black/50 text-white hover:bg-black/70"
      >
        ♡
      </button>
    </div>

    <div class="p-4">
      <h2 class="text-white font-semibold text-base mb-1 truncate">
        {{ movie.title }}
      </h2>

      <p class="text-sm mb-1">
        <span class="text-yellow-400">★ {{ movie.rating }}</span>
        <span class="text-slate-400 ml-2">{{ movie.year }}</span>
      </p>

      <p class="text-slate-400 text-xs mb-3">
        {{ movie.category }}
      </p>

      <button
        class="w-full bg-slate-800 text-white text-sm py-2 rounded-lg hover:bg-slate-700 transition-colors"
      >
        Voir le détail
      </button>
    </div>
  </div>
</template>
