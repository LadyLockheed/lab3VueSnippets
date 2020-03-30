<template>
    

    <div class="addSnippet">
        
     <div class="form">
        <label for="title">Title</label>
        <input type="text" id="title" placeholder="Title" v-model="newSnippet.title" :class="titleClass"
			@blur.once="titleIsTouched = true"/>
            <span v-if="titleIsTouched && !titleIsValid" class="error"> {{ titleErrorMessage }} </span>
        
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
       

        
    }),
    methods:{
        addNewSnippet(){
           
            let NewTitle=this.newSnippet.title
            let NewContent=this.newSnippet.content
                
                // skickar till api
            //    axios.post(this.baseUrl+"?add&title="+NewTitle+"&content="+NewContent).then((Response)=>{

            //         let test=Response
            //         console.log("Response: ",Response);
            //         console.log("Response: ",Response.data);
            //         console.log("config:", Response.config);
            //         this.newSnippet=Response.data
                
            //     })

            //tömmer inputfälten
            //TODO Title fältet blir felvaliderat när man skickat och den tömt fältet. 
            // this.newSnippet.title="";
            // this.newSnippet.content=""

            


            //=================

           fetch(this.baseUrl+"?add&title="+NewTitle+"&content="+NewContent, {
                    method: 'POST',
                })
                .then(response => response.json())
                .then((data) => {
                    
                    let snippets = data;
                    console.log("Från api: ", data);
                    
                })
                .catch((error) => {
                   
                    console.log("Error: ",error);
                 
                })



                // entireFormIsValid(){
                // if(this.titleIsValid && this.contentIsValid){
                //     fetch('https://www.forverkliga.se/JavaScript/api/api-snippets.php?add&title=' + this.model.formTitle + '&content=' + this.model.formContent , {
                //         method: 'POST'
                //     })
                //     .then((response) => {
                //         this.$emit('newSnippet', response)
                //     })
                //     .catch((error) => {
                //         this.errorMsg = 'Failed to add snippet, please try again';
                //         this.error = true;
                //         console.log(error);
                //     })
                // }
                // else{
                //     this.errorMsg = 'Enter the form properly';
                //     this.error = true;
                // }
            }
            
        
                

           
            
             
                
          
            
        }//slut addNewSnippet

    },//slut methods
    computed:{
        titleIsValid() {
			return this.newSnippet.title.length >= 1;
			
		},
		titleClass() {
			if( !this.titleIsTouched ) return '';
			return this.titleIsValid ? 'valid' : 'invalid';
		},
		titleErrorMessage() {
			return 'Your title needs to contain at least 1 character'
		},


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