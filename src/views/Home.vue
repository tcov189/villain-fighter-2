<template>
  <div class="container">
    <h1 class="text-center mb-4">Welcome to Villain Fighter 2!</h1>

    <BattleContainer
      :characters="characters"
      :image-src="imageSrc"
    />

    <section id="dialog" class="my-2 py-4">
      <div class="d-flex justify-content-center" v-if="!gameStarted">
        <button class="btn btn-success"
          @click="gameStarted = !gameStarted"
          >Start New Game</button>
      </div>

      <PlayerActions v-else-if="gameStarted && !gameOver"
        :player-specials="this.characters.all_might.specials"
        @player-attacks="playerAttacked"
        @player-special-attacks="playerSpecialAttacked"
        @player-heals="playerHeals"
        @player-gives-up="playerGivesUp"
      />

      <div class="d-flex justify-content-center" v-if="gameOver">
        <button class="btn btn-success"
          @click="startNewGame"
          >Play Again?</button>
      </div>
    </section>

    <BattleLogs
      v-if="gameStarted"
      :logs="logs"
     />
  </div>
</template>

<script>
import BattleContainer from '@/components/BattleContainer/BattleContainer.vue';
import BattleLogs from '@/components/BattleLogs.vue';
import PlayerActions from '@/components/PlayerActions.vue';

import $ from 'jquery';

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
      gameOver: false,
      characters: {
        all_might: {
          name: 'All Might',
          specials: 1,
          image: '/img/characters/all-might.png',
          health: 100,
          wins: 0,
          losses: 0,
        },
        nomu: {
          name: 'Nomu',
          specials: 1,
          image: '/img/characters/nomu-usj.png',
          health: 100,
          wins: 0,
          losses: 0,
        },
      },
      test: null,
      imageSrc: '/img/characters/specials/plus-ultra.gif',
      logs: [],
    };
  },
  methods: {
    playerAttacked(damage, wasACrit, villanDamage) {
      if (this.characters.nomu.health - damage > 0) {
        this.characters.nomu.health -= damage;
      } else {
        this.characters.nomu.health = 0;
      }

      this.logs.unshift({
        isPlayer: true,
        text: `Player hits for ${damage}! ${wasACrit ? "IT'S A CRIT!!!!" : ''}`,
      });

      if (this.checkIfGameOver()) {
        this.gameOver = true;

        this.logs.unshift({
          isPlayer: true,
          text: 'Player WINS!',
        });

        return;
      }

      if (this.characters.all_might.health - villanDamage > 0) {
        this.characters.all_might.health -= villanDamage;
      } else {
        this.characters.all_might.health = 0;
      }

      this.logs.unshift({
        isPlayer: false,
        text: `Villian hits for ${villanDamage}!`,
      });

      if (this.checkIfGameOver()) {
        this.gameOver = true;

        this.logs.unshift({
          isPlayer: false,
          text: "Villan wins :'(",
        });
      }
    },
    playerSpecialAttacked(damage, wasACrit, villanDamage) {
      this.playerAttacked(damage, wasACrit, villanDamage);

      this.characters.all_might.specials -= 1;

      $('#special-modal').modal('show');

      this.test = wasACrit;
    },
    playerHeals(villanDamage) {
      if (this.characters.all_might.health !== 100 && this.characters.all_might.health < 100) {
        this.characters.all_might.health += 10;
      }

      if (this.characters.all_might.health > 100) {
        this.characters.all_might.health = 100;
      }

      if (this.characters.all_might.health - villanDamage > 0) {
        this.characters.all_might.health -= villanDamage;
      } else {
        this.characters.all_might.health = 0;
      }

      this.logs.unshift({
        isPlayer: true,
        text: 'Player heals for 10',
      });

      this.logs.unshift({
        isPlayer: false,
        text: `Villian hits for ${villanDamage}!`,
      });

      this.checkIfGameOver();
    },
    playerGivesUp() {
      this.characters.nomu.wins += 1;
      this.characters.all_might.losses += 1;

      this.startNewGame();
    },
    checkIfGameOver() {
      let isGameOver = false;
      if (this.characters.nomu.health <= 0) {
        this.characters.all_might.wins += 1;
        this.characters.nomu.losses += 1;
        isGameOver = true;
      } else if (this.characters.all_might.health <= 0) {
        this.characters.nomu.wins += 1;
        this.characters.all_might.losses += 1;
        isGameOver = true;
      }

      return isGameOver;
    },
    startNewGame() {
      this.gameOver = false;
      this.gameStarted = true;

      this.characters.all_might.health = 100;
      this.characters.all_might.specials = 1;
      this.characters.nomu.health = 100;
      this.characters.nomu.specials = 1;

      this.logs = [];
    },
  },
  mounted() {
    $('special-modal').on('hidden.bs.modal', () => {
      this.imageSrc = '';
    });
  },
};
</script>

<style lang="scss" scoped>
#dialog {
  border: 1px solid #ccc;
  box-shadow: 0px 3px 6px #ccc;
}
</style>
