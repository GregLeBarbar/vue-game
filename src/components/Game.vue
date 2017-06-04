<template>
  <!-- On est obligé d'avoir un div englobant -->
  <div class="game">
    <span class="round" v-on:click="clickOnRound"></span>
  </div>
</template>

<script>
export default {
  name: 'game',
  methods: {
    clickOnRound: function () {
      console.log('click')
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
