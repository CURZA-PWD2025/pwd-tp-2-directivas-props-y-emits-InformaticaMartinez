<script setup lang="ts">
import { defineProps, defineEmits, ref } from "vue";
import type { Pelicula } from "../Interface/Pelicula";

const props = defineProps<{ movie: Pelicula }>();
const emit = defineEmits(["update_likes"]);
const liked = ref(false);

const toggleLike = () => {
    liked.value = !liked.value;
    emit("update_likes", props.movie.id, liked.value ? 1 : -1);
};
</script>

<template>
    <div class="card">
      <h2 class="card-title">{{ movie.titulo }} ({{ movie.anio }})</h2>
      <p class="info"><strong>Género:</strong> {{ movie.genero }}</p>
      <p class="info"><strong>Director:</strong> {{ movie.director }}</p>
  
      <div v-if="movie.portada">
        <img :src="movie.portada" :alt="`Portada de ${movie.titulo}`" />
      </div>
      <p v-else class="no-portada">🎞️ Portada no disponible</p>
  
      <button @click="toggleLike">{{ liked ? "❤️ Quitar Like" : "🤍 Dar Like" }}</button>
      <p class="likes">Likes: {{ movie.likes + (liked ? 1 : 0) }}</p>
    </div>
  </template>

<style>
.card {
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid #ffffff40;
  padding: 16px;
  margin: 8px;
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(255, 255, 255, 0.1);
  text-align: center;
  max-width: 280px;
  color: #fff;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: scale(1.03);
  box-shadow: 0 0 20px rgba(255, 255, 255, 0.3);
}

.card-title {
  font-size: 1.5rem;
  margin-bottom: 12px;
  color: #ffcc00;
  text-shadow: 1px 1px 3px black;
  font-family: 'Bebas Neue', sans-serif;
}

.info {
  margin: 4px 0;
  font-size: 1rem;
}

.likes {
  margin-top: 8px;
  font-weight: bold;
}

img {
  max-width: 100%;
  border-radius: 12px;
  margin-top: 10px;
}

button {
  margin-top: 12px;
  padding: 10px 16px;
  background-color: #e50914;
  color: #fff;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

button:hover {
  background-color: #b00610;
}

.no-portada {
  color: #f8d7da;
  background-color: rgba(255, 0, 0, 0.2);
  padding: 8px;
  border-radius: 8px;
  margin-top: 10px;
  font-style: italic;
}
</style>
