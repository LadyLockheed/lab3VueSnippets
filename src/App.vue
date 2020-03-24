<template>
  <div id="app">
  
    <Header/>
    <Latest/>
    <Popular/>
  </div>
</template>

<script>

import Header from './components/Header.vue'
import Latest from './components/Latest.vue'
import Popular from './components/Popular.vue'

export default {
  name: 'App',
  components: {
   
    Header,
    Latest,
    Popular
  }
}
</script>

<style>
#app {
  box-sizing:border-box;
  padding: 0;
  margin: 0;
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  color: #2c3e50;
  
  background-color:#595959
}
</style>
