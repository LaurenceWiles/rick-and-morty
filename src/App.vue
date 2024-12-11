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

console.log(characters);
</script>

<template>
  <div>
    <h1>Rick and Morty</h1>
    <h2>characters</h2>
    <p v-if="loading">Loading...</p>
    <p v-if="error" class="error">{{ error }}</p>
    <div class="cards-container">
      <Card
        v-for="character in characters"
        :key="character.id"
        :name="character.name"
        :status="character.status"
        :gender="character.gender"
        :image="character.image"
      />
    </div>
  </div>
</template>

<style lang="scss">
.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 16px;
  padding: 16px;
}

.error {
  color: red;
  font-weight: bold;
}
</style>
