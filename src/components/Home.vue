<template>

<div class="home">

    <h1>Kådning...de ä gött dä...</h1>
   
    <!-- <h1>Kådning...</h1>
    <h2>de ä gött dä...</h2> -->


</div>
  
</template>

<script>

export default {
    data:()=>({

        
        })

}
</script>


<style scoped>
@import url(https://fonts.googleapis.com/css?family=Roboto);
@import url(https://fonts.googleapis.com/css?family=Roboto+Mono:500&display=swap);
@import url('https://fonts.googleapis.com/css?family=Liu+Jian+Mao+Cao&display=swap');
@import url('https://fonts.googleapis.com/css?family=Indie+Flower&display=swap');
@import url('https://fonts.googleapis.com/css?family=Rasa&display=swap');
@import url('https://fonts.googleapis.com/css?family=Montserrat&display=swap');
 
.home{
    padding:3em;
    
}
h1{

    animation-name: textFadeIn;
    animation-duration: 3s;
    /* font-family:'Indie Flower', cursive; */
    /* font-family: "Rasa"; */
    font-family:'Montserrat', sans-serif;
    font-size:3.5em;
    padding-top:1.5em;
    color:#2e303f;
  
}

/* h2{
   
    animation-name: spanFadeIn;
    animation-duration: 3s;
  
    animation-delay: 6s;
    border:1px solid pink;
 
} */
@keyframes textFadeIn {
   0% { 
        opacity: 0; 
    } 
    100% { 
        opacity: 1; 
    } 
 
}
/* @keyframes spanFadeIn{
    0% { 
        opacity: 0; 
    } 
    100% { 
        opacity: 1; 
    } 

} */
    


</style>



