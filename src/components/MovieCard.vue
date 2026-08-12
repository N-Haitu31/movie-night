<script setup>
defineProps(["movie"]);
const emit = defineEmits(["toggle-favorite", "display-details-pressed"]);
</script>

<template>
  <div
    class="overflow-hidden rounded-xl bg-slate-900 shadow-lg transition-transform duration-200 hover:scale-[1.02]"
  >
    <div class="relative">
      <img
        :src="movie.image"
        :alt="movie.title"
        class="h-64 w-full object-cover"
      />
      <button
        class="absolute top-2 right-2 flex h-8 w-8 items-center justify-center rounded-full bg-black/50 text-white hover:bg-black/70"
        @click="emit('toggle-favorite', movie.id)"
      >
        ♡
      </button>
    </div>

    <div class="p-4">
      <h2 class="mb-1 truncate text-base font-semibold text-white">
        {{ movie.title }}
      </h2>

      <p class="mb-1 text-sm">
        <span class="text-yellow-400">★ {{ movie.rating }}</span>
        <span class="ml-2 text-slate-400">{{ movie.year }}</span>
      </p>

      <p class="mb-3 text-xs text-slate-400">
        {{ movie.category }}
      </p>

      <button
        class="w-full rounded-lg bg-slate-800 py-2 text-sm text-white transition-colors hover:bg-slate-700"
        @click="emit('display-details-pressed', movie.id)"
      >
        Voir le détail
      </button>
    </div>
  </div>
</template>
