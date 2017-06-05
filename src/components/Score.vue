<template>
  <div class="score">
    {{ score ? 'Votre score : ' + score : 'Entrez votre nom et appuyez sur entrée pour démarrer' }}
  </div>
</template>

<script>
export default {
  name: 'score',
  props: ['score']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .score {
    display: inline-block;
    height: 80px;
    width: 150px;
    font-size: 12pt;
    color: greenyellow;
    background: #666;
    padding: 5px;
  }
</style>
