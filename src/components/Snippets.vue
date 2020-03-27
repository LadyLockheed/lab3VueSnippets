<template>
    

    <div class="snippets">
        
        <h2 v-if="snippetsList=='Loading...'">{{snippetsList}}</h2>

        <div v-if="snippetsList!='Loading...'" class=snippetsContainer>

            <div class="snippetsContainer">
                <button @click="getLatestSnippets">Latest</button>
                <button>Popular</button>
                <button>Reported</button>

            </div>
            
            <div v-for="snippet in snippetsList" :key="snippet.id" class="list">
               
                    <h3>{{snippet.title}}</h3>
                    <p>{{snippet.content}}</p>
                    <p>{{snippet.id}}</p>
                    <button @click="saveId(snippet.id)">Knapp</button>
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
.snippetsContainer{
    background-color:darkgrey;
}

.snippets{
color:rgb(96, 56, 102);
font-family: 'Franklin Gothic Medium';


}
button{
    padding:1em;
    border-radius:1em;
    border:1px solid black;;
}
.list{
    border:2px solid #FAD9FF;
    border-radius:0.3em;
    margin:1em;
    padding:0.5em;
}
h3{
    margin-left:0em 1em 0em 2em;
    /* padding:1em; */
}
p{
    color:lightgreen;
    margin-left:0em 1em 0em 2em;
}


</style>