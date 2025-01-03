<template>
  <div class="character-card">
    <img :src="img" :alt="`${name} picture`" class="character-card__image" />
    <div class="character-card__details">
      <h3 class="character-card__name">{{ name }}</h3>
      <p class="character-card__status">Status: {{ status }}</p>
      <p class="character-card__gender">Gender: {{ gender }}</p>
    </div>
  </div>
</template>

<script setup>
defineProps({
  img: {
    type: String,
    required: true,
  },
  name: {
    type: String,
    required: true,
  },
  status: {
    type: String,
    required: true,
  },
  gender: {
    type: String,
    required: true,
  },
});
</script>

<style lang="scss">
.character-card {
  display: flex;
  flex-direction: row;
  align-items: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 0;
  background-color: #f9f9f9;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 400px;

  &__image {
    width: 50%;
    height: -webkit-fill-available;
    border-radius: 8px 0 0 8px;
    object-fit: cover;
  }

  &__details {
    margin-top: 1rem;
    width: 50%;
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

@media (max-width: 426px) {
  .character-card {
    flex-direction: column;

    &__image {
      width: 100%;
      margin-bottom: 1rem;
      border-radius: 8px 8px 0 0;
    }

    &__details {
      width: 100%;
    }
  }
}
</style>
