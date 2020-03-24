<template>
  <div id="app">
    
    <!-- <img src="./assets/Logga.svg" alt="logo"> -->
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <myHeader/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import myHeader from './components/myHeader.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    myHeader,
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
  background-color:#595959
}
</style>
