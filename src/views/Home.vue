<template>
  <div class="container">
    <h1 class="text-center">Welcome to Villain Fighter 2!</h1>

    <BattleContainer />
  </div>
</template>

<script>
import BattleContainer from '@/components/BattleContainer/BattleContainer.vue';

export default {
  name: 'Home',
  components: {
    BattleContainer,
  },
};
</script>
