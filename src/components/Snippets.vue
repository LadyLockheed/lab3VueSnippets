<template>
    

    <div class="snippets">

        <h1 v-if="!isLoading">{{currentTab}}</h1>
        <h1 v-if="isLoading">{{loadingMessage}}</h1>
        <h2>{{errorMessage}}</h2>

        <div class="tabButtonsContainer">
            
            <button @click="getSnippets('latest')" class="tabButton">Latest</button>
            <button @click="getSnippets('best')" class="tabButton">Best</button>
            <button @click="getSnippets('reported')" class="tabButton" >Reported</button>

        </div>
    
        <div class="listContainer">

            <div v-for="snippet in snippetsList" :key="snippet.id" class="list">   
                
                <div class="informationContainer">
                    <h3 class="title">{{snippet.title}}</h3>
                    <p class="content">{{snippet.content}}</p>
                    <p>Uploaded: {{snippet.upload_dt}}</p>

                    <template v-if="displayBest || displayLatest">
                        <p>Score: {{snippet.score}}</p>
                    </template>
                    
                    <template v-if="displayReported"> 
                        <p>Reported: {{snippet.is_reported}}</p>
                    </template>

                </div>

                <div class="buttonsForLatest" v-if="displayLatest ||displayBest">
           
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
    displayBest:false,
    
    displayLatest:true,
    // smallButton:"smallButtonNoClick"
    errorMessage:"",
    
   
   
 
    }),//slut data
    methods:{

      
        async getSnippets(choice){
      
            console.log("i getsnippets, choise är: ",choice);
            this.isLoading=true;
            this.errorMessage="";
            
            try{
                let response=await axios.get(this.baseUrl,{
                    // params:{latest:""}
                    params:{[choice]:""}
                });
                    console.log("Api data GET: ",response.data);
                if(choice=='latest'){

                    this.currentTab="Latest snippets"
                    this.displayReported=false
                    this.displayBest=false
                    this.displayLatest=true
                    this.isLoading=false;
                    
                    this.snippetsList=response.data
            
                }
                else if (choice=='reported'){
                    this.currentTab="Reported snippets"
                    this.displayReported=true
                    this.displayLatest=false
                    this.displayBest=false
                        this.isLoading=false;
                    this.snippetsList=response.data
                
                }
                else if (choice=='best'){
                    this.currentTab="Best snippets"

                    this.displayReported=false
                    this.displayLatest=false
                    this.displayBest=true
                        this.isLoading=false;


                    this.snippetsList=response.data
                        

                }
        
            }
            catch(error){
                console.log("Nåt blev fel: ", error);
                this.errorMessage=error
                
            }
          
            
        
        },//slut funktion getSnippets
       
       async postSnippet(snippetId, choice){
       
            console.log("ID: ",snippetId);
            console.log("Choice:",choice);
            this.isLoading=true;
            this.errorMessage="";
   
            try {
                let response=await axios.post(this.baseUrl,{[choice]:"",id:[snippetId]});
               
                    console.log("Api data POST: ",response.data);
               
                }    
            catch (error){
                this.errorMessage=error
                this.isLoading=false;
                console.log("Nåt är fel: ", error);
                
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




/* .smallButtonNoClick{
    background-color:grey;
}
.smallButtonClick{
    background-color:hotpink;
} */

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

.tabButton{
  
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
.tabButtonsContainer :first-child {

    margin-left:1.2em;
}

.tabButton:hover, .tabButton:focus, .tabButton.selected{
    background-color:#63948c;
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