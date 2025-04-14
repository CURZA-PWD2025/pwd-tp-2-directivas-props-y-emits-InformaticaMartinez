<script setup lang="ts">
import { ref } from "vue";
import CardComponent from "./components/CardComponent.vue";
import type { Pelicula } from "./Interface/Pelicula";
import moviesData from "./resource/movies.ts";
import { Icon } from "@iconify/vue";

const movies = ref<Pelicula[]>(moviesData);

const updateLikes = (id: number, change: number) => {
  const movie = movies.value.find((m) => m.id === id);
  if (movie) movie.likes += change;
};
</script>


<template>
  <div class="app-container">
    <h1 class="main-title">🎬 Cartelera de Películas</h1>
    <div class="movies-container">
      <CardComponent
        v-for="movie in movies"
        :key="movie.id"
        :movie="movie"
        @update_likes="updateLikes"
      />
    </div>
  </div>
</template>

<style scoped>
.app-container {
  padding: 2rem;
  backdrop-filter: blur(4px);
}

.main-title {
  font-size: 3rem;
  text-align: center;
  margin: 30px 0;
  font-family: 'Bebas Neue', sans-serif;
  letter-spacing: 2px;
  color: #ffcc00;
  text-shadow:
    0 0 5px #ffcc00,
    0 0 10px #ff9900,
    0 0 15px #ff6600;
}

.movies-container {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
  padding-bottom: 40px;
}
</style>