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

    <SpecialAttackModal :img-src="imageSrc" />
  </div>
</template>

<script>
import CharacterCard from './CharacterCard.vue';
import SpecialAttackModal from './SpecialAttackModal.vue';

export default {
  props: [
    'characters',
    'imageSrc',
  ],
  components: {
    CharacterCard,
    SpecialAttackModal,
  },
};
</script>

<style>

</style>
