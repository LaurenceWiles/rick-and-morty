<template>
  <div class="sort-controls">
    <label for="sort" class="sort-controls__label">Sort by:</label>
    <select
      id="sort"
      class="sort-controls__select"
      :value="sortOption"
      @change="$emit('update:sortOption', $event.target.value)"
    >
      <option value="">None</option>
      <option value="name">Name</option>
      <option value="status">Status</option>
      <option value="gender">Gender</option>
    </select>
  </div>
</template>

<script setup>
defineProps(["sortOption"]);
defineEmits(["update:sortOption"]);
</script>

<style scoped lang="scss">
.sort-controls {
  display: flex;
  align-items: center;
  gap: 0.5rem;

  &__label {
    font-size: 1rem;
    font-weight: bold;
  }

  &__select {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
    background-color: #f9f9f9;
  }
}
</style>
