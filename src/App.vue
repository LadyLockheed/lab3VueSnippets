<template>
  <div id="app">

    
 <div class="contentWrap">
    <Header @showSnippets="onSnippetClick" @showAddSnippet="onAddSnippetClick" @showHome="onHomeClick"/>

    <Home v-if="!displaySnippets && !displayAddSnippets"/>
 
    <!-- <template v-if="displaySnippets==true"> -->
      <Snippets/>
    <!-- </template> -->
    
    <template v-if="displayAddSnippets==true">
      <addSnippet/>
    </template>


 </div>
  
    

    <Footer/>
  
  </div>
</template>

<script>

import Header from './components/Header.vue'
import addSnippet from './components/addSnippet.vue'
import Snippets from './components/Snippets.vue'
import Footer from './components/Footer.vue'
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
   
    Header,
    addSnippet,
    Snippets,
    Footer,
    Home
  },

  data:()=>({
    
    displaySnippets:"",
    displayAddSnippets:"",
 
  }),
  methods:{

    onSnippetClick(value){
  
      this.displaySnippets=value;
      this.displayAddSnippets=false;
      
    },
    onAddSnippetClick(value){
  
      this.displayAddSnippets=value;
      this.displaySnippets=false;
    },
    onHomeClick(){
      this.displayAddSnippets=false;
      this.displaySnippets=false;

    }
    

  },


}
</script>

<style>
#app {

  position: relative;
  min-height: 100vh;
  background-color:#ebe6d1;

}
.contentWrap{
   padding-bottom: 2.5rem;
   
}
*{
  box-sizing:border-box;
  padding: 0;
  margin: 0;
 
}
</style>
