<template>
  <header class="flex justify-center items-center h-24 bg-red-800 mb-10">
    <div class="text-white font-mono w-full">
      <h1 class="text-center lg:text-5xl md:text-4xl text-3xl">
        <i class="fas fa-viruses" /> COVID-19 Tracker
      </h1>
      <p class="text-center text-sm font-semibold text-gray-200">
        Powered by the
        <a class="text-red-400" target="_blank" href="https://covid19api.com/"
          >COVID19</a
        >
        API
      </p>
    </div>
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Header",
});
</script>
