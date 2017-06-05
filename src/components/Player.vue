<template>
  <!-- On est obligé d'avoir un div englobant -->
  <div>
  <!-- Utilisation de la directive v-html 
  Mais attention : ne pas rendre l'ajout de HTML dynamique pour des raisons de sécurité
  C'est vous qui ajouté du HTML 
  -->
    <span v-html="welcomeMessage" :class="{ hide: !player}"></span>
    <form @submit.prevent="setPlayer" :class="{ hide: player}" class="form-inline">
      <input type="text" placeholder="Entrer votre nom" class="form-control" />
      <button type="submit" class="btn btn-default">Jouer</button>
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
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .hide {
    display: none;
  }
</style>
