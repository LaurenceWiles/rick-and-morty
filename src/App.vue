<template>
  <div>
    <h1>Rick and Morty</h1>
    <p v-if="loading">Loading...</p>
    <p v-if="error" class="error">{{ error }}</p>
    <div class="cards-container">
      <Card
        v-for="character in paginatedCharacters"
        :key="character.id"
        :name="character.name"
        :status="character.status"
        :gender="character.gender"
        :img="character.image"
      />
    </div>
    <PaginationControls
      :currentPage="currentPage"
      :totalPages="totalPages"
      @change-page="changePage"
    />
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from "vue";
import Card from "./components/Card.vue";
import PaginationControls from "./components/PaginationControls.vue";

const characters = ref([]);
const loading = ref(true);
const error = ref(null);

const currentPage = ref(1);
const itemsPerPage = 5;

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

const paginatedCharacters = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  const end = start + itemsPerPage;
  return characters.value.slice(start, end);
});

const totalPages = computed(() =>
  Math.ceil(characters.value.length / itemsPerPage)
);

const changePage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page;
  }
};
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
