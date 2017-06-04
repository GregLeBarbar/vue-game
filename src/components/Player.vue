<template>
  <!-- On est obligé d'avoir un div englobant -->
  <div v-bind:class="playerClass">
    <span>{{ welcomeMessage }}</span>
    <form>
      <input type="text" placeholder="Entrer votre nom" v-border:yellow />
      <button type="submit">Jouer</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'player',
  created: function () {
    this.playerClass = this.player ? 'player' : 'playerForm'
    this.welcomeMessage = this.player ? 'Bonjour ' + this.player + ' !' : 'Pas de joueur.'
  },
  directives: {
    border: function (el, binding) {
      el.style.borderColor = binding.arg
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.player form {
  display: none;
}
.playerForm span {
  display: none;
}
</style>
