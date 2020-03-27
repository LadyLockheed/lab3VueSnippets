<template>
    

    <div class="addSnippet">
        
     <div class="form">
        <label for="titel">Titel</label>
        <input type="text" id="titel" placeholder="Titel">
        
        <label for="snippet">Snippet</label>
        <textarea rows="20" placeholder="Ny snippet här" id="snippet" ></textarea>
     </div>
     


    </div>


</template>

<script>
export default {

    data:()=>({
       
        
    })

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
    color:#FAD9FF;
   
}


</style>