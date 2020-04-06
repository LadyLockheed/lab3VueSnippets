<template>

<div class="home">

    <h1><span class="fadeInFirst">Kådning...</span><span class="fadeInSecond">de ä gött dä...</span></h1>
   
</div>
  
</template>

<script>

export default {
    data:()=>({

        
    })

}
</script>


<style scoped>

    @import url('https://fonts.googleapis.com/css?family=Montserrat&display=swap');
    
    .home{
        padding:3em;
        
    }
    h1{
        font-family:'Montserrat', sans-serif;
        font-size:3.5em;
        padding-top:1.5em;
        color:#2e303f;
    
    }
    .fadeInFirst{
        animation-name: textFadeIn;
        animation-duration: 3s;
    }
    .fadeInSecond{
        animation-name: spanFadeIn;
        animation-duration: 3s;
    }
    @keyframes textFadeIn {
        0% { 
            opacity: 0; 
        } 
        100% { 
            opacity: 1; 
        } 
    
    }
    @keyframes spanFadeIn{
        
        0% { 
            opacity: 0; 
        
        }
        30%{
        opacity: 0; 
        
        }
        100% { 
            opacity: 1; 
        
        } 

    }


</style>



