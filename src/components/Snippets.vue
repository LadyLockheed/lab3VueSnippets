<template>
    

    <div class="snippets">
        <!--TODO ändra namn på denna template -->
        <h1>{{Welcome}}</h1>
        <p>Displayreported: {{displayReported}}</p>
        
        <h2 v-if="snippetsList=='Loading...'">{{snippetsList}}</h2>

        <div v-if="snippetsList!='Loading...'" class=snippetsContainer>

            <div class="selectButtonsContainer">
                
                <button @click="getSnippets('?latest')" class="selectButton">Latest</button>
                <button @click="getSnippets()" class="selectButton">Popular</button>
                <button @click="getSnippets('?reported')" class="selectButton" >Reported</button>

            </div>
      

            
            <div class="listContainer">


                <div v-for="snippet in snippetsList" :key="snippet.id" class="list">   
               
                    <h3>{{snippet.title}}</h3>
                    <p>{{snippet.content}}</p>
                    <p>Score: {{snippet.score}}</p>
                    <!-- <div v-if="displayReported">Rapporterad: {{snippet.is_reported}}</div> -->
                    <p>Rapporterad: {{snippet.is_reported}}</p>
                   
                    
                    
                    <div class="buttons" v-if="displayLatestSnippets">
                    
                        
                        <button @click="postSnippet(snippet.id,'?report&id=' )">Report snippet</button>
                        <button @click="postSnippet(snippet.id, '?upvote&id=')">Upvote</button>
                        <button @click="postSnippet(snippet.id, '?downvote&id=')">Downvote</button>

                    </div>
              
                </div>
            </div>
      
        </div>
     
    </div>

</template>

<script>
import axios from 'axios'
export default {

    data:()=>({
    Welcome:"Senaste snippets",
    baseUrl:"https://www.forverkliga.se/JavaScript/api/api-snippets.php",
    snippetsList:"Loading...",
    testNewList:"",
    displayReported:false,
    // reportedSnippetsList:"Loading...",
    displayLatestSnippets:true,
   
   
 
    }),//slut data
    methods:{

        getSnippets(choice){

            console.log("i getsnippets, choise är: ",choice);
            
            axios.get(this.baseUrl+choice).then((response)=>{
        
            console.log("Hämtat från api: ", response);

        
            if(choice=='?latest'){
                
                this.Welcome="Senaste snippets"
                this.displayReported=false
                this.displayLatestSnippets=true,
                this.snippetsList=response.data;
            
            }
            else if(choice=='?reported'){
                
                this.Welcome="Rapporterade snippets"
                this.displayReported=true
                this.displayLatestSnippets=false,
                this.snippetsList=response.data;
                
            }
            //TODO else if popular
           
            
            })//slut api get latest

            
        },//slut funktion getSnippets
        postSnippet(snippetId, choice){

               fetch (this.baseUrl,
            {
                method:"POST",
                body:new URLSearchParams(choice+snippetId),
               
            })
            .then((response)=>{
                console.log("PostSnippet: ", response);
                
            })
            .catch((error)=>{
                console.log("Error i postsnippet ", error);
                
            })

            this.getSnippets('?latest')


        },
     
       
    },//slut methods
    created: function (){
       this.getSnippets('?latest')
    },//slut created
    

}//slut export default


</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Montserrat&display=swap');
.snippetsContainer{
    background-color:#ebe6d1;
   
}
h1{
    margin:1em;
    color:#2e303f;
    font-family: "Montserrat";
}
h2{
    margin:1em;
    color:#c24332;
    font-family: Helvetica, monospace;
    
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
    margin:1em;
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