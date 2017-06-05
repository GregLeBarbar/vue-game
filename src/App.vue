<template>
  <div id="app">
    <game v-on:score="updateScore"></game>
    <player class="text-center"></player>
    <score :score=score class="text-center"></score>
  </div>
</template>

<script>
import Game from './components/Game'
import Score from './components/Score'
import Player from './components/Player'

export default {
  name: 'app',
  data: function () {
    return { score: 0 }
  },
  components: {
    Game,
    Score,
    Player
  },
  methods: {
    updateScore: function (score) {
      this.score = score
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 700px;
  display: block;
}
</style>
