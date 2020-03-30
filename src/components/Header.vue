<template>
 
  <div class="header">
    <img src="../assets/Logga_montserrat.svg" alt="logo" @click="handleDisplayHome">
    
    <div class="navBar">
    <!--  
      <ul>
        <li @click="handleDisplaySnippets">Snippets</li>
        <li @click="handleDisplayAddSnippet">Lägg till snippet</li>
        
      </ul> -->
      <button @click="handleDisplaySnippets">Snippets</button>
      <button @click="handleDisplayAddSnippet">Lägg till snippets</button>

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

img{
  margin-left:1em;
}
button{
  margin: 0em 1em 0;
  color:white;
  background-color:#63948c;
  border:none;
  font-size:1em;
  font-family: Helvetica, monospace;
  letter-spacing: 0.5px;	
	text-transform: uppercase;
  margin-top:0.6em;
}
button:hover, button:focus, button.selected{
  border-bottom:3px solid #c24332;
  cursor: pointer;
  outline:0;
}

</style>