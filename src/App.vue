<template>
  <div id="app">
    <AnecdotCard msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import AnecdotCard from './components/AnecdotCard.vue'

export default {
  name: 'App',
  components: {
    AnecdotCard
  }
}
</script>

<style>
body{
  margin:0;
  padding: 0;
  background-color: black;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}
</style>
