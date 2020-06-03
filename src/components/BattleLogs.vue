<template>
  <section class="row log" v-if="logs.length > 0">
      <div class="col">
          <ul class="list-unstyled">
              <li :class="{'player-turn' : log.isPlayer, 'villain-turn': !log.isPlayer}"
              v-for="(log, index) in logs"
              :key="index">
                  {{ log.text }}
              </li>
          </ul>
      </div>
  </section>
</template>

<script>
export default {
  props: [
    'logs',
  ],
};
</script>

<style lang="scss" scoped>
  .log {
    margin-top: 30px;
    text-align: center;
    padding: 10px;
    border: 1px solid #ccc;
    box-shadow: 0px 3px 6px #ccc;
    font-weight: bold;
    text-transform: uppercase;

    .player-turn {
        color: blue;
        background-color: #e4e8ff;
    }

    .villain-turn {
      color: red;
      background-color: #ffc0c1;
    }
  }
</style>
