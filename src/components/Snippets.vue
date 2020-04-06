<template>

    <div class="snippets">

        <h1 v-if="!isLoading">{{currentTab}}</h1>
        <h1 v-if="isLoading">{{loadingMessage}}</h1>
        <h2>{{errorMessage}}</h2>

        <div class="tabButtonsContainer">
            
            <button @click="getSnippets('latest')" class="inactiveTab" :class="{activeTab:latestIsActive}" :disabled="isLoading">Latest</button>
            <button @click="getSnippets('best')" class="inactiveTab" :class="{activeTab:bestIsActive}" :disabled="isLoading">Best</button>
            <button @click="getSnippets('reported')" class="inactiveTab" :class="{activeTab:reportedIsActive}" :disabled="isLoading">Reported</button>

        </div>
    
        <div class="listContainer">

            <div v-for="snippet in snippetsList" :key="snippet.id" class="list">   
                
                <div class="informationContainer">
                    <h3 class="title">{{snippet.title}}</h3>
                    <p class="content">{{snippet.content}}</p>
                    <p>Uploaded: {{snippet.upload_dt}}</p>
                    

                    <template v-if="!displayReported">
                        <p>Score: {{snippet.score}}</p>
                    </template>
             
                    <template v-if="displayReported"> 
                        <p>Reported: {{snippet.is_reported}}</p>
                    </template>

                </div>

                <div class="buttonsForLatest" v-if="!displayReported">
           
                    <button @click="postSnippet(snippet.id, 'upvote')" :disabled="isLoading">Upvote</button>
                    <button @click="postSnippet(snippet.id, 'downvote')" :disabled="isLoading">Downvote</button>
                    <button @click="postSnippet(snippet.id,'report' )" :disabled="isLoading">Report snippet</button>

                </div>
            
                <div class="buttonsForReported" v-if="displayReported">
                    
                    <button @click="postSnippet(snippet.id,'unreport')" :disabled="isLoading">Unreport</button>
                    <button @click="postSnippet(snippet.id,'delete')" :disabled="isLoading">Delete</button>
                
                </div>
            </div>
        </div>
    </div>

</template>

<script>
import axios from 'axios'
export default {

    data:()=>({
    currentTab:"",
    baseUrl:"https://www.forverkliga.se/JavaScript/api/api-snippets.php",
    snippetsList:"",
    isLoading:false,
    loadingMessage:"Loading...",
    displayReported:false,
    errorMessage:"",
    latestIsActive:"",
    bestIsActive:"",
    reportedIsActive:"",

    }),//slut data
    methods:{

        async getSnippets(choice){
    
            this.isLoading=true;
            this.errorMessage="";
        
            try{
                let response=await axios.get(this.baseUrl,{
                    params:{[choice]:""}
                });
                   
                if(choice=='latest'){

                    this.currentTab="Latest snippets"
                    this.displayReported=false
                    this.latestIsActive=true;
                    this.reportedIsActive=false;
                    this.bestIsActive=false;
            
                }
                else if (choice=='reported'){
                    this.currentTab="Reported snippets"
                    this.displayReported=true
                    this.reportedIsActive=true;
                    this.latestIsActive=false;
                    this.bestIsActive=false;
              
                }
                else if (choice=='best'){
                    this.currentTab="Best snippets"
                    this.displayReported=false
                    this.bestIsActive=true;
                    this.latestIsActive=false;
                    this.reportedIsActive=false;
              
                }
                    this.snippetsList=response.data
                    this.isLoading=false;
        
            }
            catch(error){
                this.errorMessage=error
                
            }
           
          
            
        
        },//slut funktion getSnippets
       
       async postSnippet(snippetId, choice){
    
            this.isLoading=true;
            this.errorMessage="";
   
            try{
               await axios.post(this.baseUrl,{[choice]:"",id:snippetId});
         
            }    
            catch (error){
                this.errorMessage=error
                this.isLoading=false;
          
            }
            finally{
                this.isLoading=false;
            }

            if(this.currentTab=="Latest snippets"){
                this.getSnippets("latest")
            }
            else if(this.currentTab=="Reported snippets"){
                this.getSnippets("reported")
        
            }
            else if(this.currentTab=="Best snippets"){
                this.getSnippets("best") 
            }
    
        },
     
       
    },//slut methods
    created: function (){
       this.getSnippets('latest')
    },//slut created
    

}//slut export default


</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Montserrat&display=swap');
.snippetsContainer{
    background-color:#ebe6d1;
    
}
.inactiveTab{
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
.inactiveTab:disabled{
    color:#cca28f;

}
.tabButtonsContainer :first-child {
    margin-left:1.2em;
}
.inactiveTab:hover, .inactiveTab:focus, .inactiveTab.selected{
    background-color:#63948c;
}
.activeTab{
    border:2px solid #63948c;
    border-radius:0.3em 0.3em 0 0;
    background-color:#63948c;
    color:white;
    letter-spacing: 0.5px;	
	text-transform: uppercase;
    font-weight:bold;
    padding:0.7em;
    margin-top:2em;
}
.list{
    border-radius:0.3em;
    margin:0.5em;
    padding:1em;
    background-color:white;
    display:grid;
    grid-template-columns: repeat(15, 1fr);
    grid-template-rows:auto;
}
.informationContainer{
    grid-column:1/15;
}
.buttonsForLatest{
    grid-column-end:16;
}
.buttonsForLatest > button{
    padding:0.3em;
    margin:0.2em;
    margin-top:2em;
    border:none;
    border: 2px solid #2e303f;
    border-radius:0.3em;
    width:6em;
    background-color:#63948c;
    color:white;
}
.buttonsForLatest > button:nth-child(3){
    padding:0.3em;
    margin:0.3em;
    margin-top:1em;
    border:none;
    border-radius:0.3em;
    width:12.3em;
    background-color:#c24332;
    color:white;
    display:block;
}
.buttonsForLatest > button:hover {
    cursor:pointer;
}
.buttonsForLatest > button:disabled {
	background-color: #d39891;
	color: lightgray;
}
.buttonsForReported>button:hover{
    cursor:pointer;
}
.buttonsForReported >button:disabled{
    background-color: #d39891;
    color: lightgray;
}
.buttonsForReported{
    grid-column-end:16;
    margin-top:1em;
}
.buttonsForReported >button{
    padding:0.3em;
    margin:0.2em;
    border:none;
    border-radius:0.3em;
    width:6em;
    background-color:#63948c;
    color:white;
}
.buttonsForReported > button:nth-child(2){
    background-color:#c24332;
}
h1{
    margin:0.5em 1em 0.5em 0.5em;
    color:#2e303f;
    font-family: "Montserrat";
}
h2{
    margin:1em;
    color:#c24332;
    font-family: Helvetica, monospace;
}
.title{
    font-family: Helvetica, monospace;
    color:#2e303f;
    margin:0;
}
.loadingMsg{
    display:inline-block;
}
.content{
    font-size:1em;
    border-radius:0.3em;
    padding:0.3em;
    margin:0.5em 2em 1em 0em;
    margin-bottom:0.3em;
    background-color:#ebe6d1
}
.snippets{
    color:white;
    font-family: Helvetica, monospace;
    padding:1em;
}
.listContainer{
    background-color:#63948c;
    border-radius:0 1em 1em 1em;
    padding:1em;
    margin:0 1em 1em 1em;
}
h3{
    margin-left:0em 1em 0em 2em;
    color:#2e303f;
}
p{
    color:#2e303f;
    margin-left:0em 1em 0em 2em;
}

</style>