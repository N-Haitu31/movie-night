<script setup>
const emit = defineEmits(["navigate"]);

const { favoriteCount } = defineProps({
  favoriteCount: {
    type: Number,
    required: true,
    default: 0,
  },
});

function navigateTo(view) {
  emit("navigate", view);
}
</script>

<template>
  <header
    class="flex max-w-7xl flex-col gap-4 border-b border-slate-800 bg-slate-950/95 px-4 py-5 sm:flex-row sm:items-center sm:justify-between"
  >
    <button class="text-left text-xl font-black tracking-tight text-white">
      MOVIE NIGHT
    </button>
     <nav class="flex items-center gap-2">
       <button
         class="rounded-full bg-rose-500 px-4 py-2 text-sm font-semibold text-white transition"
         @click="navigateTo('films')"
       >
         Films
       </button>
       <button
         class="rounded-full px-4 py-2 text-sm font-semibold text-slate-300 transition hover:bg-slate-800"
         @click="navigateTo('favorites')"
       >
         Favoris {{ favoriteCount }}
       </button>
     </nav>
  </header>
</template>
