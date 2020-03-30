<template>
 
  <div class="header">
    <img src="../assets/Logga_montserrat.svg" alt="logo" @click="handleDisplayHome">
    
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
      console.log("Klick på image funkar");
      
      this.$emit("showHome")

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
  background-color:#63948c;


}
.navBar{

  margin-top:0.3em;
  margin-left:0.5em;
  color:white;
  font-size:1.2em;
  font-family: Helvetica, monospace;
	letter-spacing: 0.5px;	
	text-transform: uppercase;

  
 
}
img{
  margin-left:1em;
}
li:hover{
  
    border-bottom:3px solid white;

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
  margin: 1em 1em 0em 1em;
  padding-bottom:0.5em;
  
  
}


</style>