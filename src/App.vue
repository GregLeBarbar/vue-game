<template>
  <div id="app">
    <game></game>
    <score></score>
    <player></player>
  </div>
</template>

<script>
import Game from './components/Game'
import Score from './components/Score'
import Player from './components/Player'

export default {
  name: 'app',
  components: {
    Game,
    Score,
    Player
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
