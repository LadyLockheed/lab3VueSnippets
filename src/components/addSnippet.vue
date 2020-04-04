<template>
    
<!-- TODO Fixa så att meddelande visas medans ny snippet laddas upp. OCh klar meddeleande vissa när man lyckats -->
<!-- TODO Lägg valideringsmeddelandet i ett span för att det ska dyka upp brevid formuläret (om det får plats). Kanske dålig ide om sidan ska mobilanpassas, hmm -->
<!-- TODO Kanske validera hela formuläret på en gång istället genom att klicka på knappen -->
<!-- TODO ändra muspekaren -->
    <div class="addSnippet">
    <h2>{{errorMessage}}</h2>
        
     <div class="form">
        <label for="title">Title</label>
        <!-- <input type="text" id="title" placeholder="Title" v-model="newSnippet.title" :class="titleClass"
			@blur.once="titleIsTouched = true"/>
            <span v-if="titleIsTouched && !titleIsValid" class="error"> {{ titleErrorMessage }} </span> -->

            <input type="text" id="title" placeholder="Title" v-model="newSnippet.title" 
			@blur.once="titleIsTouched = true"/>
            
            
            <p class="valid">{{validmessage}}</p>
        
        
        
        <label for="snippet">Snippet</label>
        <textarea rows="20" placeholder="Ny snippet här" id="snippet" v-model="newSnippet.content"></textarea>
        Listan: {{newSnippet}}
        <button @click="addNewSnippet">Save snippet</button>
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
       errorMessage:"",
       validmessage:"Du gjorde fel"
       

        
    }),
    methods:{
       
       async addNewSnippet(){

           //TODO validering. Använd computed properties för att kolla om flera validreringsgrejer är ok, returnera true eller false till submitknappen.

            let NewTitle=this.newSnippet.title
            let NewContent=this.newSnippet.content
    
            try {
                 let response=await axios.post(this.baseUrl,
                     {add:"", title:NewTitle, content:NewContent});
              
                    console.log("Från api: ", response.data);
                    console.log("Detta är i axios");
            } 
            catch (error){
                this.errorMessage=error
                console.log("Nåt är fel: ", error);
                
            }


               
    
               
            
        }//slut addNewSnippet

    },//slut methods
    computed:{
        // titleIsValid() {
		// 	return this.newSnippet.title.length >= 1;
			
		// },
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


.addSnippet{
   padding:1em;
   
}
.form{
    display:grid;
    
    border: 1px solid gray;
	border-radius: 1em;
    padding:1em;
    margin:1em;

}
.form>input{
    margin:0em 1em 0.3em 1em;
    padding:0.5em;
    border-radius:0.3em;
    border:3px solid lightblue;
    width:70%
  
}
.form >textarea{
    margin:0em 1em 1em 1em;
    padding:0.5em;
    display:block;
     border-radius:0.3em;
     border:3px solid lightblue;
      width:70%
}
.form>label{
    margin:0.5em 0em 0.4em 0.8em;
    color:rgb(133, 111, 136);
    font-family: Helvetica, monospace;
   
}
input.valid { border-color: green; }
input.invalid { border-color: red; }
.error {
	color: red;
	font-size: 90%;
}
button{
    padding:0.5em;
    font-family: Helvetica, monospace;
    margin:1em;
    width:70%;
    border-radius:0.3em;
    border:2px solid #63948c;
 
}
.valid{
    display:inline-block;
}
@media (max-width: 600px)  {
    button{
        color:hotpink;
    }

}

</style>