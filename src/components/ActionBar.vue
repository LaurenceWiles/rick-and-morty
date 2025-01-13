<template>
  <div class="action-bar">
    <SearchBar
      :searchTerm="searchTerm"
      @update:searchTerm="(value) => $emit('update:searchTerm', value)"
    />
    <SortControls
      :sortOption="sortOption"
      @update:sortOption="(value) => $emit('update:sortOption', value)"
    />
    <button
      class="action-bar__favorites-button"
      @click="$emit('open-favorites')"
    >
      View Favorites
    </button>
  </div>
</template>

<script setup>
import SearchBar from "./SearchBar.vue";
import SortControls from "./SortControls.vue";

defineProps(["searchTerm", "sortOption"]);
defineEmits(["update:searchTerm", "update:sortOption", "open-favorites"]);
</script>

<style lang="scss" scoped>
.action-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background-color: #eaeaea;
  border: 1px solid #ccc;
  gap: 1rem;
  margin-bottom: 3rem;

  &__search input {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  &__sort select {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  &__favorites-button {
    padding: 0.5rem 1rem;
    border: 1px solid #ccc;
    background-color: #f9f9f9;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;

    &:hover {
      background-color: #007bff;
      color: white;
    }
  }

  @media (max-width: 426px) {
    flex-wrap: wrap;
    justify-content: center;
    margin-bottom: 1rem;

    &__search,
    &__sort,
    &__favorites {
      flex: 1 1 100%;
      text-align: center;
      margin-bottom: 0.5rem;
    }

    &__search input,
    &__sort select,
    &__favorites button {
      width: 90%;
      max-width: 300px;
    }
  }
}
</style>
