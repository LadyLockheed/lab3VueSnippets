<template>
    

    <div class="addSnippet">
        
     <div class="form">
        <label for="title">Title</label>
        <input type="text" id="title" placeholder="Title" v-model="newSnippet.title">
        
        <label for="snippet">Snippet</label>
        <textarea rows="20" placeholder="Ny snippet här" id="snippet" v-model="newSnippet.content"></textarea>
        Listan: {{newSnippet}}
     </div>
     
        <button></button>

    </div>


</template>

<script>
export default {

    data:()=>({
       newSnippet:{id:null, title:"", content:""},
        
    }),


}
</script>
<style scoped>

.addSnippet{
   
}
.form{
    display:grid;
    /* grid-template-columns: 1fr */
    border: 1px solid gray;
	border-radius: 1em;
    padding:1em;
    margin:1em;
    /* grid-template-columns: repeat(10, 5em);
    grid-template-rows: auto; */


}
.form>input{
    margin:0em 1em 0.3em 1em;
    padding:0.5em;
    border-radius:0.3em;
    /* display:block; */
    /* max-width:300px; */
    /* width:40em; */
    
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


</style>