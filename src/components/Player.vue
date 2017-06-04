<template>
  <!-- On est obligé d'avoir un div englobant -->
  <div>
    <span v-hide>{{ welcomeMessage }}</span>
    <form v-hide>
      <input type="text" placeholder="Entrer votre nom" v-border:yellow />
      <button type="submit">Jouer</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'player',
  created: function () {
    this.player = 'Grégory'
    this.playerClass = this.player ? 'player' : 'playerForm'
    this.welcomeMessage = this.player ? 'Bonjour ' + this.player + ' !' : 'Pas de joueur.'
  },
  directives: {
    border: function (el, binding) {
      el.style.borderColor = binding.arg
    },
    // creation de la directive custom 'hide'
    hide: function (el, binding, vnode) {
      let player = vnode.context.player
      let isForm = vnode.tag === 'form'
      if (isForm) {
        el.style.display = player ? 'none' : 'block'
      } else {
        el.style.display = player ? 'block' : 'none'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
