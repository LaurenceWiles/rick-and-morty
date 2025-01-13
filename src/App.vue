<template>
  <div>
    <h1>Rick and Morty</h1>
    <ActionBar
      v-model:searchTerm="searchTerm"
      v-model:sortOption="sortOption"
      :favorites="favorites"
      @open-favorites="openFavorites"
    />
    <p v-if="loading">Loading...</p>
    <p v-if="error" class="error">{{ error }}</p>
    <FavoritesModal
      :favorites="favorites"
      :isOpen="isFavoritesModalOpen"
      @close="isFavoritesModalOpen = false"
    />
    <div class="cards-container">
      <Card
        v-for="character in paginatedCharacters"
        :key="character.id"
        :id="character.id"
        :name="character.name"
        :status="character.status"
        :gender="character.gender"
        :img="character.image"
        :isFavorite="isFavorite(character.id)"
        @toggle-favorite="toggleFavorite"
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
import ActionBar from "./components/ActionBar.vue";
import FavoritesModal from "./components/FavoritesModal.vue";

const characters = ref([]);
const loading = ref(true);
const error = ref(null);

const searchTerm = ref("");
const sortOption = ref("");
const favorites = ref([]);
const isFavoritesModalOpen = ref(false);

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

const toggleFavorite = (character) => {
  const index = favorites.value.findIndex((fav) => fav.id === character.id);
  if (index !== -1) {
    favorites.value.splice(index, 1);
  } else {
    favorites.value.push(character);
  }
};

const isFavorite = (id) =>
  favorites.value.some((character) => character.id === id);

const filteredCharacters = computed(() => {
  let result = characters.value;

  if (searchTerm.value) {
    result = result.filter((character) =>
      character.name.toLowerCase().includes(searchTerm.value.toLowerCase())
    );
  }

  if (sortOption.value) {
    result = [...result].sort((a, b) =>
      a[sortOption.value].localeCompare(b[sortOption.value])
    );
  }

  return result;
});

const paginatedCharacters = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  const end = start + itemsPerPage;
  return filteredCharacters.value.slice(start, end);
});

const totalPages = computed(() =>
  Math.ceil(filteredCharacters.value.length / itemsPerPage)
);

const changePage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page;
  }
};

const openFavorites = () => {
  isFavoritesModalOpen.value = true;
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

@media (max-width: 426px) {
  h1 {
    font-size: 2rem;
  }
}
</style>
