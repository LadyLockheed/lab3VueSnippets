<template>
    

    <div class="snippets">
        
        <h2 v-if="snippetsList=='Loading...'">{{snippetsList}}</h2>

        <template v-if="snippetsList!='Loading...'">
            
            <div v-for="snippet in snippetsList" :key="snippet.id" class="list">
                    <h3>{{snippet.title}}</h3>
                    <p>{{snippet.content}}</p>
                    <p>{{snippet.id}}</p>
                    <button @click="saveId(snippet.id)">Knapp</button>
            </div>
    
        </template>
                
        
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

.snippets{
color:rgb(96, 56, 102);
;

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