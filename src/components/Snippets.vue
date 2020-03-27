<template>
    

    <div class="snippets">
        
            <div v-for="snippet in snippetsList" :key="snippet.id" class="list">
               <h3>{{snippet.title}}</h3>
               <p>{{snippet.content}}</p>
               <p>{{snippet.id}}</p>
               <button @click="saveId(snippet.id)">Knapp</button>
            </div>
        
        
    </div>


</template>

<script>
import axios from 'axios'
export default {

    data:()=>({
    baseUrl:"https://www.forverkliga.se/JavaScript/api/api-snippets.php",
    snippetsList:[],
        snippets:[
            {id: 1, titel: "For-loop", snippet:"for (i=0)"},
            {id: 2, titel: "If-sats", snippet:"if (villkor)"},
            {id: 3, titel: "Border", snippet:"1px solid green"},
            {id: 4, titel: "Grid", snippet:"display:grid"},
            {id: 5, titel: "Flex", snippet:"display:flex"},
            {id: 6, titel: "Block", snippet:"display:block"},
            {id: 7, titel: "Inline-block", snippet:"display:inline-block"},
            {id: 8, titel: "Data i vue", snippet:"data:()=>({})"},
            {id: 9, titel: "Methods", snippet:"methods:{}"},
            {id: 10, titel: "Computed", snippet:"computed:{}"},
            
        ]
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
color:#FAD9FF;


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