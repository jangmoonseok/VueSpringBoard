<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <FreeBoard/>
</template>

<script>
import FreeBoard from './components/PAGE/FreeBoard.vue';

export default {
  name: 'App',
  components: {
    FreeBoard
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
