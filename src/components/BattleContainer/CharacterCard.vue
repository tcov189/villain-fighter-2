<template>
  <div class="character-card">
    <div class="character-info-container d-flex flex-column align-items-center">
      <p class="font-weight-bold h4 mb-0">{{ character.name }}</p>
      <p>{{ characterWinLoss }}</p>
      <img class="img-fluid" :src="character.image" :alt="`${character.name} image`" />
    </div>

    <div class="health-bar-container">
      <div class="progress mt-1">
        <div
          class="progress-bar"
          role="progressbar"
          :style="{
              width: `${character.health}%`,
              backgroundColor: healthBarColor,
              color: healthBarTextColor
          }"
          :aria-valuenow="character.health"
          aria-valuemin="0"
          aria-valuemax="100"
        >{{ character.health }}%</div>
      </div>
    </div>

    <div class="specials-container">
      Specials left:
      <div class="d-flex justify-content-between">
        <div
          class="special-icon d-flex p-1 justify-content-center"
          v-for="(special, index) in specials"
          :key="`special_${index}`"
        >
          <span aria-hidden="true" class="fas fa-bolt"></span>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  props: ['character'],
  data() {
    return {
      wins: 0,
      losses: 0,
      specials: this.character.specials,
    };
  },
  computed: {
    characterWinLoss() {
      return `${this.wins} - ${this.losses}`;
    },
    healthBarColor() {
      let color = 'green';
      if (this.character.health <= 40 && this.character.health > 20) {
        color = 'yellow';
      } else if (this.character.health <= 20) {
        color = 'red';
      }
      return color;
    },
    healthBarTextColor() {
      let color = 'white';

      if (this.character.health <= 40 && this.character.health > 20) {
        color = 'black';
      } else if (this.character.health <= 20) {
        color = 'white';
      }
      return color;
    },
  },
};
</script>

<style lang="scss" scoped>
.special-icon {
  border: 1px solid black;
  background-color: blue;
  color: white;
  flex-basis: 26px;
  font-weight: bold;
}

img {
  max-height: 300px;
}

.progress {
  border-radius: 0%;
  height: 30px;
  background-color: #cecccc;

  .progress-bar {
    background-color: green
  }
}
</style>
