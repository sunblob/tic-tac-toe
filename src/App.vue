<template>
  <div id="app">
    <Game />
  </div>
</template>

<script>
import Game from '@/components/Game'

export default {
  components: {
    Game
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
