<template>
    
<!-- TODO Fixa så att meddelande visas medans ny snippet laddas upp. OCh klar meddeleande vissa när man lyckats -->
<!-- TODO Lägg valideringsmeddelandet i ett span för att det ska dyka upp brevid formuläret (om det får plats). Kanske dålig ide om sidan ska mobilanpassas, hmm -->
<!-- TODO Kanske validera hela formuläret på en gång istället genom att klicka på knappen -->
<!-- TODO ändra muspekaren -->
    <div class="addSnippet">

        <h1 v-if="!isLoading">{{headline}}</h1>
        <h1 v-if="isLoading">{{loadingMessage}}</h1>
        <h2>{{errorMessage}}</h2>
        
        <div class="form">
            <!-- Title -->
            <label for="title">Title</label>
            <input type="text" id="title" placeholder="Title" v-model="newSnippet.title" @blur.once="titleIsTouched=true" />
          
            <p class="invalidTitle" v-if="!titleIsValid && titleIsTouched">{{invalidMsg}}</p>
            
            <!-- Content -->
            <label for="content">Snippet</label>
            <textarea rows="3" placeholder="New snippet here" id="content" v-model="newSnippet.content" @blur.once="contentIsTouched=true"></textarea>
            
            <p class="invalidContent" v-if="!contentIsValid && contentIsTouched">{{invalidMsg}}</p>
           
            <!-- Submit -->
            <button @click="addNewSnippet" :disabled="!contentIsValid || !titleIsValid || isLoading">Save snippet</button>
             <!-- <p>Listan: {{newSnippet}}</p> -->

             <h2 v-if="isAdded">New snippet added!</h2>
        </div>
     
        

    </div>


</template>

<script>
import axios from 'axios'
export default {

    data:()=>({
       newSnippet:{id:null, title:"", content:""},
       baseUrl:"https://www.forverkliga.se/JavaScript/api/api-snippets.php",
       titleIsTouched: false,
       contentIsTouched:false,
       errorMessage:"",
       invalidMsg:"Dont forget to write something here",
       headline:"Add your snippet",
       isLoading:false,
       isAdded:false,
       loadingMessage:"Loading..."
      
       

        
    }),
    methods:{
       
       async addNewSnippet(){
           this.isAdded="";
           this.isLoading=true;

           //TODO validering. Använd computed properties för att kolla om flera validreringsgrejer är ok, returnera true eller false till submitknappen.

            let NewTitle=this.newSnippet.title
            let NewContent=this.newSnippet.content
    
            try {
                 let response=await axios.post(this.baseUrl,
                     {add:"", title:NewTitle, content:NewContent});
              
                    console.log("Från api: ", response.data);
                   
                    this.isAdded=true;
                    this.isLoading=false;
            } 
            catch (error){
                this.errorMessage=error
                console.log("Nåt är fel: ", error);
                this.isLoading=false;
                
            }


               
    
               
            
        }//slut addNewSnippet

    },//slut methods
    computed:{
        titleIsValid() {
			return this.newSnippet.title.length >= 1;
			
        },
        contentIsValid(){
            return this.newSnippet.content.length >= 1;
        }
		// titleClass() {
		// 	if( !this.titleIsTouched ) return '';
		// 	return this.titleIsValid ? 'valid' : 'invalid';
		// },
		// titleErrorMessage() {
		// 	return 'Your title needs to contain at least 1 character'
		// },


    }

     

}//slut export default
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Montserrat&display=swap');

.addSnippet{
   padding:1em;
   
}
h1{
    margin:0.5em 1em 1em 0.8em;
    color:#2e303f;
    font-family: "Montserrat";
}
.form{
 
    border: 3px solid #63948c;
	border-radius: 1em;
    padding:1em;
    margin:1em;
    font-family: Helvetica, monospace;

}
.form > h2{
 margin-left:0.5em;
  color:#2e303f;
 
}
.form>input{
    margin:0em 1em 0.3em 1em;
    padding:0.5em;
    border-radius:0.3em;
    border:2px solid #8ec9bf;
    width:70%;
    display:inline-block;
}
.form >textarea{
    margin:0em 1em 0.3em 1em;
    resize: none;
    padding:0.5em;
    display:inline-block;
    border-radius:0.3em;
    border:2px solid #8ec9bf;
    width:70%
}
.form>label{
    margin:0.5em 0em 0.4em 0.8em;
    color:rgb(133, 111, 136);
    /* font-family: Helvetica, monospace; */
    display:block;
   
}
.invalidTitle{
    display:inline-block;
    border:2px solid #c24332;
    padding:0.3em;
    /* font-family: Helvetica, monospace; */

}
.invalidContent{
    display:inline-block;
    border:2px solid #c24332;
    padding:0.3em;
    /* font-family: Helvetica, monospace; */


}


button{
    padding:0.5em;
    /* font-family: Helvetica, monospace; */
    margin:1em;
    margin-top:3em;
    width:70%;
    border-radius:0.3em;
    border:none;
    background-color:#63948c;
    color:white;
 
}
button:hover{
    cursor:pointer;
}
button:disabled{
    background-color: #8ec9bf;
    color:rgb(172, 172, 172);
}

@media (max-width: 600px)  {
    button{
        color:hotpink;
    }

}

</style>