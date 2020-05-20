<template>
  <div class="d-flex flex-column" id="batte-container">
    <div class="row">
      <div class="col">
        <CharacterCard :character="characters.all_might" />
      </div>
      <div class="col">
        <CharacterCard :character="characters.nomu" />
      </div>
    </div>
  </div>
</template>

<script>
import CharacterCard from './CharacterCard.vue';

export default {
  props: [
    'characters',
  ],
  components: {
    CharacterCard,
  },
};
</script>

<style>

</style>
