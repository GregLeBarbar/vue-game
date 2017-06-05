<template>
  <!-- On est obligé d'avoir un div englobant -->
  <div class="content">
    <div class="game" @click="clickOnInterface" :class="{ wait: !player }">
      <!-- j'ai remplacé la touche alt par la touche ctrl car alt ne fonctionnait pas -->
      <span v-if="player" class="round" :style="roundStyle" :class="{bonus: bonusActivated, badColor: badColorActivated}" @click.stop="clickOnRound" @click.ctrl.stop="bonus"></span>
    </div>
    <div class="log">
      <p v-for="item in userLogs" v-if="item.type === 'user'">
        #{{ item.id }} - {{ item.msg }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'game',
  props: ['player'],
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
  computed: {
    userLogs: function () {
      return this.collection.filter(
        function (item) {
          return item.type === 'user'
        })
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
      this.$emit('score', this.click)
    }
  },
  methods: {
    clickOnRound: function (event) {
      setTimeout(this.updateRound, 1000)
      this.updateClick(true)
      this.addLog(`BRAVO !`)
    },
    updateClick: function (increment) {
      if (!this.player) {
        return
      }

      if (increment) {
        this.click++
      } else {
        this.click--
      }
    },
    bonus: function (event) {
      if (this.bonusActivated) {
        this.updateClick(true)
        this.addLog(`PERFECT ! +2`)
      } else {
        this.updateClick()
        this.addLog(`???? -1`)
      }
    },
    clickOnInterface: function (event) {
      this.updateClick()
      this.addLog(`HO NON :( -1`)
    },
    start: function (event) {
      if (event.key === 'Enter') {
      }
    },
    updateRound: function () {
      let size = Math.random() * (100 - 10) + 10
      let top = Math.random() * (60 - 5) + 5
      let left = Math.random() * (60 - 5) + 5

      this.badColorActivated = size < 20
      this.bonusActivated = size > 80

      this.addLog({
        size: size,
        top: top,
        left: left
      }, 'round')

      this.roundStyle.height = this.roundStyle.width = `${size}px`
      this.roundStyle.margin = `${top}% ${left}%`
    },
    addLog: function (msg, type) {
      if (!this.player) {
        return
      }

      let typeOfMsg = type || 'user'
      this.collection.unshift({id: this.collection.length / 2, msg: msg, type: typeOfMsg})
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
  opacity: 1;
  transition: opacity 1s;
}

.round {
  background: aliceblue;
  border-radius: 9999px;
  position: absolute;
  transition: width 2s, height 2s, margin 0.5s;
}

.bonus {
  background: indianred;
}

.badColor {
  background: #2A4747;
}

.wait {
  opacity: 0.3;
}

</style>
