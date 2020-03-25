<template>
 
  <div class="header">
    <img src="../assets/Logga.svg" alt="logo">
    
    <div class="navBar">
 
      <ul>
        <li @click="handleDisplaySnippets">Snippets</li>
        <li @click="handleDisplayAddSnippet">Lägg till snippet</li>
      </ul>
  
    </div>
    

  </div>


</template>

<script>
export default {

  data:()=>({
    
    displaySnippets:"",
    displayAddSnippet:""
        
  }),
  methods:{
    handleDisplaySnippets(){
      console.log("klick funkar");
   
    },
    handleDisplayAddSnippet(){
      console.log("klick 2 funkar");
      
    }
  }

}

</script>
<style scoped>

.header{
  display:flex;
  flex-direction:row;
  padding:0.5em;
  justify-content:space-between;

}
.navBar{

  margin-top:0.3em;
  margin-left:0.5em;
  color: #FAD9FF;
  font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  font-size:1em;
 
}
li:hover{
    border-bottom:4px solid #FAD9FF;
    
}
.active{
    border-bottom:4px solid #FAD9FF;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
  
}

</style>