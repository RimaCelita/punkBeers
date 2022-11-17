<template>
  <beer-info></beer-info>
</template>

<script>
import BeerInfo from './components/BeerInfo'

export default {
  name: 'App',
  components: {
    BeerInfo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
