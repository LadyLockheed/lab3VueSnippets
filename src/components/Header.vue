<template>
 
  <div class="header">
    <img src="../assets/Logga.svg" alt="logo" @click="handleDisplayHome">
    
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
    
   
        
  }),
  methods:{
    handleDisplaySnippets(){
 
      let displaySnippets=true;
      
      this.$emit("showSnippets", displaySnippets) // skickar till app

    },
    handleDisplayAddSnippet(){
  
      let displayAddSnippet=true;
      this.$emit("showAddSnippet", displayAddSnippet)

    },
    handleDisplayHome(){


    }
 
  }

}

</script>
<style scoped>

.header{
  display:flex;
  flex-direction:row;
  padding:1em;
  justify-content:space-between;
  background-color:#595959


}
.navBar{

  margin-top:0.3em;
  margin-left:0.5em;
  color: #FAD9FF;
  font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  font-size:1.2em;
  font-weight: bold;
  padding-bottom:1em;
 
}
img{
  margin-left:1em;
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
  margin: 1em 1em 0 1em;
  
}


</style>