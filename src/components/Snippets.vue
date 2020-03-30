<template>
    

    <div class="snippets">
        
        <h2 v-if="snippetsList=='Loading...'">{{snippetsList}}</h2>

        <div v-if="snippetsList!='Loading...'" class=snippetsContainer>

            <div class="selectButtonsContainer">
                <button @click="getLatestSnippets" class="selectButton">Latest</button>
                <button class="selectButton">Popular</button>
                <button class="selectButton">Reported</button>

            </div>
            <div class="listContainer">

                <div v-for="snippet in snippetsList" :key="snippet.id" class="list">
               
                    <h3>{{snippet.title}}</h3>
                    <p>{{snippet.content}}</p>
                    <p>{{snippet.id}}</p>
                    <button @click="saveId(snippet.id)" class="idButton">Knapp</button>
            </div>
            </div>
      
        </div>
     
    </div>

</template>

<script>
import axios from 'axios'
export default {

    data:()=>({

    baseUrl:"https://www.forverkliga.se/JavaScript/api/api-snippets.php",
    snippetsList:"Loading...",
 
    }),//slut data
    methods:{

        saveId(snippetId){
            console.log("Sparat id är: ",snippetId);
            
        },
        getLatestSnippets(){
            console.log("Getlastest snippets klick funkar");
            
            axios.get(this.baseUrl+"?latest").then((Response)=>{
        
            console.log("Hämtat från api: ", Response);
            console.log("Hämtat från api, data:", Response.data);
        
            this.snippetsList=Response.data;
  
            })//slut api get latest

        }//slut funktion getLatestSnippets
  
        
    },//slut methods
    created: function (){
       
        axios.get(this.baseUrl+"?latest").then((Response)=>{
        
        console.log("Hämtat från api: ", Response);
        console.log("Hämtat från api, data:", Response.data);
        
        this.snippetsList=Response.data;
       
        
  
    })//slut api get latest

    }//slut created
}//slut export default


</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Montserrat&display=swap');
.snippetsContainer{
    background-color:#ebe6d1;
   
}
h2{
    color:#2e303f
}

.snippets{
color:white;
font-family: Helvetica, monospace;

}
.listContainer{
    
    background-color:#63948c;
    border-radius:0.5em;
    padding:0.5em;
    margin:0 1em 1em 1em;


}
.selectButton{
  
    border:2px solid #63948c;
    border-radius:0.3em 0.3em 0 0;
    background-color:#ebe6d1;
    color:#2e303f;
    letter-spacing: 0.5px;	
	text-transform: uppercase;
    font-weight:bold;
    padding:0.7em;
    margin-top:2em;

}
.selectButtonsContainer :first-child {

    margin-left:2.5em;
}

.selectButton:hover, .selectButton:focus, .selectButton.selected{
    background-color:#63948c;
}
.idButton{
    padding:1em;
    border-radius:1em;
     border:1px solid grey;
}
.list{
    
    border-radius:0.3em;
    margin:0.5em;
    padding:0.5em;
    background-color:white;
}
h3{
    margin-left:0em 1em 0em 2em;
    color:#2e303f;

    /* padding:1em; */
}
p{
    color:#2e303f;
    margin-left:0em 1em 0em 2em;
}


</style>