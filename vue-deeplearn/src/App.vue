<template>
  <div id="app">
    <img src="./assets/logo.png">
    <DeepLearning/>
  </div>
</template>

<script>
import DeepLearning from './components/DeepLearning'

export default {
  name: 'App',
  components: {
    DeepLearning
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
