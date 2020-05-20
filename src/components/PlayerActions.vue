<template>
  <div class="d-flex justify-content-around">
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
    <button @click="giveUp" class="btn btn-secondary" id="give-up">
      <i class="fas fa-sad-tear"></i>&nbsp;Give Up
    </button>
  </div>
</template>

<script>
export default {
  props: [
    'playerSpecials',
  ],
  methods: {
    attack() {
      const damage = this.calculateDamage(5, 12);

      this.$emit('player-attacks', damage);
    },
    specialAttack() {
      const damage = this.calculateDamage(17, 25);

      this.$emit('player-special-attacks', damage);
    },
    heal() {
      this.$emit('player-heals');
    },
    giveUp() {
      this.$emit('player-gives-up');
    },
    calculateDamage(min, max) {
      const isCrit = Math.max(Math.floor(Math.random() * 10 + 1), 1) === 1;
      const damage = Math.max(Math.floor(Math.random() * max) + 1, min);

      return isCrit ? Math.ceil(max * 1.5) : damage;
    },
  },
};
</script>

<style>
</style>
