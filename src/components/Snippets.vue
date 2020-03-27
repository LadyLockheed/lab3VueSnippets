<template>
    

    <div class="snippets">
        
            <div v-for="snippet in snippets" :key="snippet.id" class="list">
               <h3>{{snippet.titel}}</h3>
               <p>{{snippet.snippet}}</p>
               <p>{{snippet.id}}</p>
               <button @click="saveId(snippet.id)">Knapp</button>
            </div>
        
    </div>


</template>

<script>
export default {

    data:()=>({

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
    }),
    methods:{

        saveId(snippetId){
            console.log("Sparat id är: ",snippetId);
            
        }
    }

}
</script>
<style scoped>

.snippets{
color:#FAD9FF;

}
.list{
    border:2px solid lightcoral;
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