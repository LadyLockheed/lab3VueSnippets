<template>
    
<div class="header">
 <img src="../assets/Logga.svg" alt="logo">
    <nav>
      <ul>
        <li>Senaste</li>
        <li>Topplista</li>
        <li>Lägg till snippet</li>
        <li>Rapporterade snippets</li>
        <li>Logga in</li>
      </ul>

    </nav>
   

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
  justify-content: space-around;
}

.li:hover{
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