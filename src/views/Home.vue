<template>
  <div class="container">
    <h1 class="text-center">Welcome to Villain Fighter 2!</h1>

    <BattleContainer />

    <section id="dialog" class="my-2 py-4">
      <div class="d-flex justify-content-center" v-if="!gameStarted">
        <button class="btn btn-success"
          @click="gameStarted = !gameStarted"
          >Start New Game</button>
      </div>

      <PlayerActions v-else />
    </section>
  </div>
</template>

<script>
import BattleContainer from '@/components/BattleContainer/BattleContainer.vue';
import PlayerActions from '@/components/PlayerActions.vue';

export default {
  name: 'Home',
  components: {
    BattleContainer,
    PlayerActions,
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
  border: 1px solid #ccc;
  box-shadow: 0px 3px 6px #ccc;
}
</style>
