<script setup>
const props = defineProps({
  movie: {
    type: Object,
    required: true,
    default: () => ({}),
  },
});
</script>

<template>
  <article
    class="max-h-[90vh] w-full max-w-3xl overflow-y-auto rounded-3xl border border-slate-700 bg-slate-900 shadow-2xl"
  >
    <div class="grid md:grid-cols-[260px_1fr]">
      <img
        :src="movie.image"
        :alt="movie.title"
        class="h-full w-full object-cover"
      />

      <div class="p-6 sm:p-8">
        <div class="flex items-start justify-between gap-4">
          <div>
            <p
              class="text-sm font-bold tracking-[0.2em] text-rose-400 uppercase"
            >
              {{ movie.category }}
            </p>
            <h2 class="mt-2 text-3xl font-black text-white">
              {{ movie.title }}
            </h2>
          </div>

          <button
            class="grid h-10 w-10 shrink-0 place-items-center rounded-full bg-slate-800 text-white hover:bg-slate-700"
            aria-label="Fermer"
          >
            ×
          </button>
        </div>

        <div class="mt-5 flex flex-wrap gap-3 text-sm text-slate-300">
          <span> {{ movie.year }} </span>

          <span> • </span>
          <span> {{ movie.duration }} </span>
          <span> • </span>

          <span class="font-bold text-amber-400"> ★ {{ movie.rating }} </span>
        </div>

        <p class="mt-6 leading-7 text-slate-300">
          {{ movie.description }}
        </p>

        <div class="mt-8 flex flex-wrap gap-3">
          <button
            class="rounded-full bg-rose-500 px-5 py-2.5 text-sm font-semibold text-white transition hover:bg-rose-400"
          >
            Ajouter aux favoris
          </button>
          <button
            class="rounded-full bg-white px-5 py-2.5 font-bold text-slate-950 hover:bg-rose-100"
          >
            Fermer
          </button>
        </div>
      </div>
    </div>
  </article>
</template>
