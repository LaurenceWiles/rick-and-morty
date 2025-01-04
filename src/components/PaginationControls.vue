<template>
  <div class="pagination">
    <button
      class="pagination__button"
      @click="$emit('change-page', currentPage - 1)"
      :disabled="currentPage === 1"
    >
      Previous
    </button>
    <span class="pagination__span"
      >Page {{ currentPage }} of {{ totalPages }}
    </span>
    <button
      class="pagination__button"
      @click="$emit('change-page', currentPage + 1)"
      :disabled="currentPage === totalPages"
    >
      Next
    </button>
  </div>
</template>

<script setup>
defineProps({
  currentPage: {
    type: Number,
    required: true,
  },
  totalPages: {
    type: Number,
    required: true,
  },
});
</script>

<style lang="scss">
.pagination {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 1rem;
  gap: 1rem;

  &__button {
    min-width: 100px;
    padding: 0.5rem 1rem;
    border: 1px solid #ccc;
    background-color: #eaeaea;
    border-radius: 4px;
    cursor: pointer;
    text-align: center;

    &:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }
  }

  &__span {
    font-size: 1rem;
  }
}

@media (max-width: 426px) {
  .pagination {
    &__button {
      min-width: 75px;
      font-size: 0.75rem;
    }
    &__span {
      font-size: 0.75rem;
    }
  }
}
</style>
