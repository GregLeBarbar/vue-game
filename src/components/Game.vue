<template>
  <!-- On est obligé d'avoir un div englobant -->
  <div class="game" @click="clickOnInterface">
    <!-- j'ai remplacé la touche alt par la touche ctrl car alt ne fonctionnait pas -->
    <span class="round" ref="round" @click.stop="clickOnRound" @click.ctrl.stop="bonus"></span>
  </div>
</template>

<script>
export default {
  name: 'game',
  data: function () {
    return {
      click: 0
    }
  },
  created: function () {
    // this.start est une méthode
    document.onkeydown = this.start
    console.log(this)
  },
  watch: {
    click: function () {
      this.updateRound()
    }
  },
  methods: {
    clickOnRound: function (event) {
      this.click++
    },
    bonus: function (event) {
      console.log('BONUS')
      console.log(event)
    },
    clickOnInterface: function (event) {
      console.log('INTERFACE')
      console.log(event)
    },
    start: function (event) {
      if (event.key === 'Enter') {
        console.log('START')
      }
    },
    updateRound: function () {
      let element = this.$refs.round
      let size = Math.random() * (100 - 10) + 10
      let top = Math.random() * (60 - 5) + 5
      let left = Math.random() * (60 - 5) + 5
      element.style.height = element.style.width = `${size}px`
      element.style.margin = `${top}% ${left}%`
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
