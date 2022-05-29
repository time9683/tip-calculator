
<script>
import { tips } from "../store";

export let number;
export let des;
</script>


<div>


    <label for={number}  class={$tips === number ? 'active' : ''} >

        {number}%
     
        
    </label>
    
    <input  id={number}  class="input-num"  type="radio" name="tip" on:change      checked={des === true ?  false :  ''}  bind:value={number} >

    </div>



<style>

    * {
        font-family: 'Epilogue', sans-serif;
    }


input[type="radio"] {
  display: none;
}


label{
    box-sizing: border-box;
padding: 6px 10px;
background-color:  hsl(183, 100%, 15%);
color:white;
font-size: 16px;
font-weight: bold;
border-radius: 6px;
/* min-width: 110px; */
display:inline-block;
text-align: center;
padding: 10% 35%;
}

/* if input is cheked the label background is red */

 label.active{

background-color: hsl(172, 67%, 45%);
color: hsl(183, 100%, 15%);

 }



 label:hover{
     cursor: pointer;
     color: hsl(183, 100%, 15%);;
     background-color: hsl(172, 67%, 45%);
 }



</style>