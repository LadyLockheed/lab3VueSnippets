<template>
    

    <div class="addSnippet">
        
     <div class="form">
        <label for="title">Title</label>
        <!-- <input type="text" id="title" placeholder="Title" v-model="newSnippet.title" :class="titleClass"
			@blur.once="titleIsTouched = true"/>
            <span v-if="titleIsTouched && !titleIsValid" class="error"> {{ titleErrorMessage }} </span> -->

            <input type="text" id="title" placeholder="Title" v-model="newSnippet.title" 
			@blur.once="titleIsTouched = true"/>
        
        
        
        <label for="snippet">Snippet</label>
        <textarea rows="20" placeholder="Ny snippet här" id="snippet" v-model="newSnippet.content"></textarea>
        Listan: {{newSnippet}}
        <button @click="addNewSnippet">Save snippet</button>
     </div>
     
        

    </div>


</template>

<script>
// import axios from 'axios'
export default {

    data:()=>({
       newSnippet:{id:null, title:"", content:""},
       baseUrl:"https://www.forverkliga.se/JavaScript/api/api-snippets.php",
       titleIsTouched: false,
       failToUploadmsg:""
       

        
    }),
    methods:{
        addNewSnippet(){
           
            let NewTitle=this.newSnippet.title
            let NewContent=this.newSnippet.content
                
                // skickar till api 
                //!Min gamla kod med axios, utan body och tags
            //    axios.post(this.baseUrl+"?add&title="+NewTitle+"&content="+NewContent).then((Response)=>{

            //         let test=Response
            //         console.log("Response: ",Response);
            //         console.log("Response: ",Response.data);
            //         console.log("config:", Response.config);
            //         this.newSnippet=Response.data
                
            //     })
            //     .catch ((error)=> {
            //         console.log("Error: ", error);
            //         this.failToUploadmsg="Lyckades inte ladda upp";
                    
                    
            //     })
            //!SLut min gamla kod med axios utan body och tag
            //! Test ny kod från Jonas, med fetch
              fetch (this.baseUrl,
              {
                  method:"POST",
                  body: new URLSearchParams("?add&title="+NewTitle+"&content="+NewContent+"&tags=tagUrIt"),
              
              })
              .then((response)=>{
                  console.log("Response från api: ", response);
                  
              })
              .catch((error)=>{
                console.log("Error please try again: ", error);

              })

            //tömmer inputfälten
            //TODO Title fältet blir felvaliderat när man skickat och den tömt fältet. 
            // this.newSnippet.title="";
            // this.newSnippet.content=""

            


            //=================
            //!Jonas kod med fetch som funkar att posta. HAr med body och tags
                // fetch('https://www.forverkliga.se/JavaScript/api/api-snippets.php', {
                //         method: 'POST',
                //         body: new URLSearchParams('add&title=' + this.model.formTitle + '&content=' + this.model.formContent + '&tags=tag1'),
                //     })
                //     .then((response) => {
                //         this.waitingForApi(false),
                //         this.$emit('newSnippet', response)
                //     })





        //    fetch(this.baseUrl+"?add&title="+NewTitle+"&content="+NewContent, {
        //             method: 'POST',
                    
        //         })
        //         .then(response => response.json())
        //         .then((data) => {
                    
        //             let snippets = data;
        //             console.log("Från api: ", data);
                    
        //         })
        //         .catch((error) => {
                   
        //             console.log("Error: ",error);
                 
        //         })



        
            
        
                

           
            
             
                
          
            
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
  
}
.form >textarea{
    margin:0em 1em 1em 1em;
    padding:0.5em;
    display:block;
     border-radius:0.3em;
     border:3px solid lightblue;
}
.form>label{
    margin:0.5em 0em 0.4em 0.8em;
    color:rgb(133, 111, 136);
   
}
input.valid { border-color: green; }
input.invalid { border-color: red; }
.error {
	color: red;
	font-size: 90%;
}

</style>