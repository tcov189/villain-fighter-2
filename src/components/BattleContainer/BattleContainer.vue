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
  components: {
    CharacterCard,
  },
  data() {
    return {
      characters: {
        all_might: {
          name: 'All Might',
          specials: 1,
          image: '/img/characters/all-might.png',
        },
        nomu: {
          name: 'Nomu',
          specials: 1,
          image: '/img/characters/nomu-usj.png',
        },
      },
    };
  },
};
</script>

<style>

</style>
