<template>
  <div class="score">
    {{ score ? 'Votre score : ' + score : 'Appuyez sur entrée pour démarrer' }}
  </div>
</template>

<script>
export default {
  name: 'score',
  data: function () {
    return {
      score: 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
