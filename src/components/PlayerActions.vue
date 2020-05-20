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
export default {};
</script>

<style>
</style>
