<script setup>
import { ref, onMounted } from "vue";

const characters = ref([]);
const loading = ref(true);
const error = ref(null);

onMounted(async () => {
  try {
    const response = await fetch(" https://rickandmortyapi.com/api/character");
    const data = await response.json();
    characters.value = data.results;
  } catch (err) {
    error.value = "Failed to fetch data";
  } finally {
    loading.value = false;
  }
});

console.log(characters);
</script>

<template>
  <div>
    <h1>Rick and Morty</h1>
    <h2>characters</h2>
    <ul>
      <li v-for="character in characters" :key="character.id">
        <p>{{ character.name }}</p>
      </li>
    </ul>
    <p v-if="loading">Loading...</p>
    <p v-if="error" class="error">{{ error }}</p>
  </div>
</template>

<style scoped></style>
