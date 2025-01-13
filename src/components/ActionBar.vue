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
    <div class="action-bar__favorites">
      <button>View Favorites</button>
    </div>
  </div>
</template>

<script setup>
import SearchBar from "./SearchBar.vue";
import SortControls from "./SortControls.vue";

defineProps(["searchTerm", "sortOption"]);
defineEmits(["update:searchTerm", "update:sortOption"]);
</script>

<style lang="scss" scoped>
.action-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background-color: #eaeaea;
  border-bottom: 1px solid #ccc;
  gap: 1rem;

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

  &__favorites button {
    padding: 0.5rem 1rem;
    border: none;
    background-color: #007bff;
    color: white;
    border-radius: 4px;
    cursor: pointer;

    &:hover {
      background-color: #0056b3;
    }
  }

  @media (max-width: 426px) {
    flex-wrap: wrap;
    justify-content: center;

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
