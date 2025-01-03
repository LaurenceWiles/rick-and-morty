<template>
  <h1>Rick and Morty</h1>
  <p v-if="loading">Loading...</p>
  <p v-if="error" class="error">{{ error }}</p>
  <div class="cards-container">
    <Card
      v-for="character in characters"
      :key="character.id"
      :name="character.name"
      :status="character.status"
      :gender="character.gender"
      :img="character.image"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Card from "./components/Card.vue";

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
</script>

<style lang="scss">
.cards-container {
  display: flex;
  max-width: 100%;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1.5rem;
}

.error {
  color: red;
  font-weight: bold;
}
</style>
