<template>
  <div class="search-bar">
    <input
      type="text"
      placeholder="Search characters..."
      :value="searchTerm"
      @input="$emit('update:searchTerm', $event.target.value)"
      class="search-bar__input"
    />
  </div>
</template>

<script setup>
defineProps(["searchTerm"]);
defineEmits(["update:searchTerm"]);
</script>

<style scoped lang="scss">
.search-bar {
  display: flex;
  justify-content: center;

  &__input {
    padding: 0.5rem;
    width: 100%;
    max-width: 300px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
}
</style>
