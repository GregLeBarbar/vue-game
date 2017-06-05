<template>
  <!-- On est obligé d'avoir un div englobant -->
  <div>
  <!-- Utilisation de la directive v-html 
  Mais attention : ne pas rendre l'ajout de HTML dynamique pour des raisons de sécurité
  C'est vous qui ajouté du HTML 
  -->
    <span v-html="welcomeMessage" v-hide></span>
    <form v-hide @submit.prevent="setPlayer">
      <input type="text" placeholder="Entrer votre nom" v-border:yellow />
      <button type="submit">Jouer</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'player',
  data: function () {
    return {
      player: '',
      welcomeMessage: ''
    }
  },
  updated: function () {
    this.welcomeMessage = `Bonjour <span class="player"> ${this.player}  </span> !`
  },
  methods: {
    setPlayer: function (event) {
      let playerName = event.target[0].value
      if (!playerName) {
        window.alert('Merci de renseigner votre nom')
        // pour que l'exécution s'arrête ici
        return
      }
      this.player = playerName
    }
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
