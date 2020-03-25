<template>
  <div id="app">
  
    <Header/>
    <addSnippet/>
    <Snippets/>
  </div>
</template>

<script>

import Header from './components/Header.vue'
import addSnippet from './components/addSnippet.vue'
import Snippets from './components/Snippets.vue'

export default {
  name: 'App',
  components: {
   
    Header,
    addSnippet,
    Snippets,
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
  
  /* color: #2c3e50; */
  
  background-color:#595959
}
</style>
