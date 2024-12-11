<template>
  <div class="character-card">
    <img :src="img" :alt="`${name} picture`" class="character-card__image" />
    <div class="character-card__details">
      <h3 class="character-card__name">{{ name }}</h3>
      <p class="character-card__status">{{ status }}</p>
      <p class="character-card__gender">{{ gender }}</p>
    </div>
  </div>
</template>

<script setup>
defineProps({
  img: {
    type: String,
    Required: true,
  },
  name: {
    type: String,
    Required: true,
  },
  status: {
    type: String,
    Required: true,
  },
  gender: {
    type: String,
    Required: true,
  },
});
</script>

<style lang="scss">
.character-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 1rem;
  background-color: #f9f9f9;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  max-width: 200px;
  text-align: center;

  &__image {
    width: 100%;
    height: auto;
    border-radius: 8px;
    object-fit: cover;
  }

  &__details {
    margin-top: 1rem;
  }

  &__name {
    font-size: 1.2rem;
    font-weight: bold;
  }

  &__status,
  &__gender {
    font-size: 0.9rem;
    color: #555;
  }
}
</style>
