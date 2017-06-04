<template>
  <!-- On est obligé d'avoir un div englobant -->
  <div class="game">
    <!-- j'ai remplacé la touche alt par la touche ctrl car alt ne fonctionnait pas -->
    <span class="round" v-on:click="clickOnRound" v-on:click.ctrl="bonus"></span>
  </div>
</template>

<script>
export default {
  name: 'game',
  created: function () {
    // this.start est une méthode 
    document.onkeydown = this.start
  },
  methods: {
    clickOnRound: function (event) {
      console.log('CLICK')
      console.log(event)
    },
    bonus: function (event) {
      console.log('BONUS')
      console.log(event)
    },
    start: function (event) {
      if (event.key === 'Enter') {
        console.log('BONUS')
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.game {
  width: 100%;
  height: 50%;
  display: block;
  background: darkslategrey;
}

.round {
  width: 50px;
  height: 50px;
  background: aliceblue;
  border-radius: 9999px;
  position: absolute;
  margin: 20% 20%;  
}

</style>
