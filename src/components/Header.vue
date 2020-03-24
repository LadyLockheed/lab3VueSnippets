<template>
    

    <div class="header">
<img src="../assets/Logga.svg" alt="logo">
<div class="navBar">
 
    <nav>
      <ul>
        <li><a href="Latest">Senaste</a></li>
        <li><a href="Popular">Topplista</a></li>
        <li><a href="AddSnippet">Lägg till snippet</a></li>
        <li><a href="Reported">Rapportereade snippets</a></li>
        <li><a href="Login">Logga in</a></li>
      </ul>

    </nav>
   

</div>

    </div>


</template>

<script>
export default {

    data:()=>({

        
    })

}
</script>
<style scoped>

.header{
  display:flex;
  flex-direction:row;
  padding:0.5em;

}
.navBar{

  margin-top:0.3em;
  margin-left:0.5em;
  color: #FAD9FF;
  border:2px solid green;
  font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
 
}
a{
  text-decoration:none;
  color:#FAD9FF;
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