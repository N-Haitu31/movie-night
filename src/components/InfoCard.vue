<script setup>
defineProps(["title", "message", "buttonLabel"]);
defineEmits(["action"]);
</script>

<template>
  <div
    class="mx-auto mt-16 flex max-w-md flex-col items-center gap-2 rounded-xl border border-slate-700 bg-slate-900 px-8 py-10 text-center"
  >
    <h2 class="text-lg font-semibold text-white">{{ title }}</h2>
    <p class="text-sm text-slate-400">{{ message }}</p>
    <button
      class="mt-4 rounded-lg bg-rose-500 px-5 py-2 text-sm font-medium text-white transition-colors hover:bg-pink-600"
      @click="$emit('action')"
    >
      {{ buttonLabel }}
    </button>
  </div>
</template>
