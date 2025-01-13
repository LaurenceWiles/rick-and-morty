<template>
  <div class="favorites-modal" v-if="isOpen">
    <div class="favorites-modal__overlay" @click="$emit('close')"></div>
    <div class="favorites-modal__content">
      <h2>Favorites</h2>
      <ul class="favorites-modal__list">
        <li
          v-for="favorite in favorites"
          :key="favorite.id"
          class="favorites-modal__item"
        >
          <img
            :src="favorite.img"
            :alt="`${favorite.name} picture`"
            class="favorites-modal__image"
          />
          <span>{{ favorite.name }}</span>
        </li>
      </ul>
      <button class="favorites-modal__close" @click="$emit('close')">
        Close
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps(["favorites", "isOpen"]);
defineEmits(["close"]);
</script>

<style scoped lang="scss">
.favorites-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

  &__overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
  }

  &__content {
    position: relative;
    background: white;
    padding: 2rem;
    border-radius: 8px;
    max-width: 500px;
    width: 100%;
    text-align: center;
  }

  &__list {
    list-style: none;
    padding: 0;
  }

  &__item {
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
  }

  &__image {
    width: 40px;
    height: 40px;
    margin-right: 1rem;
    border-radius: 50%;
  }

  &__close {
    padding: 0.5rem 1rem;
    border: none;
    background-color: #ff4d4d;
    color: white;
    border-radius: 4px;
    cursor: pointer;
  }
}
</style>
