<template>
  <div class="container">
    <h1 class="text-center">Welcome to Villain Fighter 2!</h1>

    <BattleContainer :characters="characters" />

    <section id="dialog" class="my-2 py-4">
      <div class="d-flex justify-content-center" v-if="!gameStarted">
        <button class="btn btn-success"
          @click="gameStarted = !gameStarted"
          >Start New Game</button>
      </div>

      <PlayerActions v-else
        :player-specials="this.characters.all_might.specials"
        @player-attacks="playerAttacked"
        @player-special-attacks="playerSpecialAttacked"
        @player-heals="playerHeals"
        @player-gives-up="playerGivesUp"
      />
    </section>

    <BattleLogs v-if="gameStarted" />
  </div>
</template>

<script>
import BattleContainer from '@/components/BattleContainer/BattleContainer.vue';
import BattleLogs from '@/components/BattleLogs.vue';
import PlayerActions from '@/components/PlayerActions.vue';

export default {
  name: 'Home',
  components: {
    BattleContainer,
    PlayerActions,
    BattleLogs,
  },
  data() {
    return {
      gameStarted: false,
      characters: {
        all_might: {
          name: 'All Might',
          specials: 1,
          image: '/img/characters/all-might.png',
          health: 100,
        },
        nomu: {
          name: 'Nomu',
          specials: 1,
          image: '/img/characters/nomu-usj.png',
          health: 100,
        },
      },
      test: null,
    };
  },
  methods: {
    playerAttacked(damage, wasACrit, villanDamage) {
      if (this.characters.nomu.health - damage > 0) {
        this.characters.nomu.health -= damage;
      } else {
        this.characters.nomu.health = 0;
      }

      if (this.characters.all_might.health - villanDamage > 0) {
        this.characters.all_might.health -= villanDamage;
      } else {
        this.characters.all_might.health = 0;
      }

      this.test = wasACrit;
    },
    playerSpecialAttacked(damage, wasACrit, villanDamage) {
      this.playerAttacked(damage, wasACrit, villanDamage);

      this.characters.all_might.specials -= 1;

      this.test = wasACrit;
    },
    playerHeals() {
      if (this.characters.all_might.health !== 100) {
        this.characters.all_might.health += 10;
      }
    },
    playerGivesUp() {

    },
  },
};
</script>

<style lang="scss" scoped>
#dialog {
  border: 1px solid #ccc;
  box-shadow: 0px 3px 6px #ccc;
}
</style>
