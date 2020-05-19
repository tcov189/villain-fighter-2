<template>
  <div class="container">
    <h1 class="text-center">Welcome to Villain Fighter 2!</h1>

    <BattleContainer />

    <section id="dialog" class="d-flex justify-content-center border border-dark my-2 py-4">
      <button class="btn btn-success" v-if="!gameStarted">Start New Game</button>

      <PlayerActions v-else />
    </section>
  </div>
</template>

<script>
import BattleContainer from '@/components/BattleContainer/BattleContainer.vue';

export default {
  name: 'Home',
  components: {
    BattleContainer,
  },
  data() {
    return {
      gameStarted: false,
    };
  },
};
</script>

<style lang="scss" scoped>
#dialog {
  border-radius: 4px;
}
</style>
