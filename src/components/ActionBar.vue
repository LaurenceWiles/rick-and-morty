<template>
  <div class="action-bar">
    <div class="action-bar__search">
      <input type="text" placeholder="Search characters..." />
    </div>
    <div class="action-bar__sort">
      <select>
        <option value="">Sort By</option>
        <option value="name">Name</option>
        <option value="status">Status</option>
        <option value="gender">Gender</option>
      </select>
    </div>
    <div class="action-bar__favorites">
      <button>View Favorites</button>
    </div>
  </div>
</template>

<script setup></script>

<style lang="scss">
.action-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background-color: #eaeaea;
  border-bottom: 1px solid #ccc;

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
}
</style>
