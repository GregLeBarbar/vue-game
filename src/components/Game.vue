<template>
  <!-- On est obligé d'avoir un div englobant -->
  <div class="content">
    <div class="game" @click="clickOnInterface">
      <!-- j'ai remplacé la touche alt par la touche ctrl car alt ne fonctionnait pas -->
      <span class="round" :style="roundStyle" :class="{bonus: bonusActivated, badColor: badColorActivated}" @click.stop="clickOnRound" @click.ctrl.stop="bonus"></span>
    </div>
    <div class="log">
      <p v-for="item in collection">
        {{ item }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'game',
  data: function () {
    return {
      click: 0,
      roundStyle: {
        height: '50px',
        width: '50px',
        margin: '20% 20%'
      },
      bonusActivated: false,
      badColorActivated: false,
      collection: []
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
      this.collection.unshift(`BRAVO ! (${this.click})`)
    },
    bonus: function (event) {
      if (this.bonusActivated) {
        this.click++
        this.collection.unshift(`PERFECT ! (${this.click}) +2`)
      } else {
        this.click--
        this.collection.unshift(`???? (${this.click}) -1`)
      }
    },
    clickOnInterface: function (event) {
      this.click--
      this.collection.unshift(`HO NON :( (${this.click}) -1`)
    },
    start: function (event) {
      if (event.key === 'Enter') {
        console.log('START')
      }
    },
    updateRound: function () {
      let size = Math.random() * (100 - 10) + 10
      let top = Math.random() * (60 - 5) + 5
      let left = Math.random() * (60 - 5) + 5

      this.badColorActivated = size < 20
      this.bonusActivated = size > 80

      this.roundStyle.height = this.roundStyle.width = `${size}px`
      this.roundStyle.margin = `${top}% ${left}%`
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.content {
  height: 500px;
}
.log {
  width: 100%;
  height: 30px;
  background: #666;
  display: block;
  overflow: hidden;
  padding: 6px;
}
.game {
  width: 100%;
  height: 90%;
  display: block;
  background: black;
}

.round {
  background: aliceblue;
  border-radius: 9999px;
  position: absolute;
}

.bonus {
  background: indianred;
}

.badColor {
  background: #2A4747;
}

</style>
