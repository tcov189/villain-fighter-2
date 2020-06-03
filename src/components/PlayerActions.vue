<template>
  <div class="d-flex justify-content-around">
    <template v-if="showBattleActions">
      <button @click="attack" class="btn btn-danger" id="attack">
        <i class="fas fa-fist-raised"></i>&nbsp;Attack
      </button>

      <button
        @click="specialAttack"
        v-if="playerSpecials > 0"
        class="btn btn-info"
        id="special-attack"
      >
        <i class="fas fa-bolt"></i>&nbsp;Special Attack
      </button>

      <button @click="heal" class="btn btn-success" id="heal">
        <i class="fas fa-plus-square"></i>&nbsp;Heal
      </button>

      <button
        @click="showBattleActions = !showBattleActions"
        class="btn btn-secondary"
        id="give-up"
      >
        <i class="fas fa-sad-tear"></i>&nbsp;Give Up
      </button>
    </template>
    <template v-else>
      <div class="d-flex flex-column">
        <p>Do you want to give up?</p>
        <div class="d-flex justify-content-between">
          <button
            class="btn btn-primary" @click="showBattleActions = !showBattleActions">NO!</button>
          <button class="btn btn-secondary" @click="playerGivesUp">yeah :'(</button>
        </div>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  props: ['playerSpecials'],
  data() {
    return {
      hitWasACrit: false,
      showBattleActions: true,
    };
  },
  methods: {
    attack() {
      const damage = this.calculateDamage(5, 12);
      const villianDamage = this.calculateDamage(5, 12);

      this.$emit('player-attacks', damage, this.hitWasACrit, villianDamage);
    },
    specialAttack() {
      const damage = this.calculateDamage(17, 25);
      const villianDamage = this.calculateDamage(5, 12);

      this.$emit(
        'player-special-attacks',
        damage,
        this.hitWasACrit,
        villianDamage,
      );
    },
    heal() {
      const villianDamage = this.calculateDamage(5, 12);
      this.$emit('player-heals', villianDamage);
    },
    playerGivesUp() {
      this.showBattleActions = true;
      this.$emit('player-gives-up');
    },
    calculateDamage(min, max) {
      this.hitWasACrit = Math.floor(Math.random() * 10 + 1) === 1;

      const damage = Math.max(Math.floor(Math.random() * max + 1), min);

      return this.hitWasACrit ? Math.ceil(max * 1.5) : damage;
    },
  },
};
</script>

<style>
</style>
