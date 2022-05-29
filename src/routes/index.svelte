<script>

import  NumberChex  from "../componetns/BoxNumber.svelte"
import {tips,bill,Npeople, desative} from "../store"


let tipAmount   = 0
let totalAmount = 0

function changeTip(e){
 
  desative.set(false)
    tips.set(e.target.value)
    console.log("change",e.target.value)
    setTimeout(()=>{
      e.target.checked = true
    })
    
    
}


function des(){
    desative.set(true)
    
}



function Reset(){
    tips.set(0)
    bill.set(0)
    Npeople.set(0)
}


$ : {

   if($bill === 0 || $Npeople === 0 || $Npeople == undefined || $bill == undefined){
       tipAmount = 0.00.toFixed(2)
       totalAmount = 0.00.toFixed(2)
      
   }else{

     tipAmount =  (($bill * ($tips/100)) / $Npeople).toFixed(2)
     totalAmount = (($bill + (tipAmount * $Npeople)) / $Npeople).toFixed(2)

   }

   
 
 

}


</script>


<main>

  <div class="title_container">


  
    <h1><img src="/logo.svg" alt="logo spli tter"></h1>


    </div>



    <div class="container">



      <div class="subcontainer">
<label class="text-input">
      <span class="subtitle">
          Bill
          </span>
     <input type="number"   bind:value={$bill}/>
     <img class="icon-input" src='/icon-dollar.svg' alt="">
 </label>   



  <span class="subtitle">Select Tip % </span>

    <label for="tips" class="label_tip">
    <NumberChex  number={5} des={$desative} on:change={changeTip} />
    <NumberChex number={10} des={$desative} on:change={changeTip} />
    <NumberChex number={15} des={$desative} on:change={changeTip} />
    <NumberChex number={25} des={$desative}  on:change={changeTip}/>
    <NumberChex number={50} des={$desative}  on:change={changeTip} />   




<!-- <label    on:click={des}> -->
  <!-- Custom -->
     <input  on:input={(e)=>{  tips.set(e.target.value)  }} class="custom_label" placeholder="Custom"  type="text" name="tip" >
  
     
  <!-- </label> -->


</label>




<label for="" class="text-input">

  <span class="subtitle">

    Number of people

  </span>

<span class="input_error"  style={$Npeople !== 0 ? "display:none": ''}>
  cant be 0
  </span>


<input  style={$Npeople === 0 ? "border:1px solid red": ''}  type="number" name=""   bind:value={$Npeople}  id="">
<img class="icon-input" src='/icon-person.svg' alt="">


</label>

</div>








<div class="display">



<div class="amount">


<p>
  Tip Amount
  
 <span>

   / person
 </span> 

</p>



  <span>
  ${tipAmount}
</span>

</div>



<div class="amount">
  <p>
  Total
  <span>
  / person:
  </span>
 </p>


   <span>${totalAmount}

   </span>



</div>





<button class="btn"  on:click={Reset}>


  Reset

</button>





</div>





</div>


</main>













<style>

  * {
    font-family: 'Epilogue', sans-serif;
    box-sizing: border-box
  }

 h1{
   margin: 0;

  text-align: center;
   font-size: 25px;
   font-weight: 400;
   color: hsl(183, 100%, 15%);
  }
 

  .title_container{
    padding: 25px;
  }

  main{

  min-height: 100vh;
  width: 100%;
  background-color: hsl(185, 41%, 84%)
  }

  .container{
   
    background-color: white;
    width: 100%;
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;
    padding: 30px;
    min-height:calc(100vh - 102px);

  }


  span{
      display: block;
  }


    .attribution { font-size: 11px; text-align: center; }
    .attribution a { color: hsl(228, 45%, 44%); }



.btn{
  background-color: hsl(172, 67%, 45%);
  border: none;
  padding: 15px;
  margin-top: 15px;
        color: rgb(0,71,75);
        border-radius: 8px;
        max-width:300px;
        text-transform: uppercase;

}


.display{
  box-sizing: border-box;

display: flex;
background-color: rgb(0,71,75);
flex-direction: column;
align-items: stretch;
border-radius: 10px;
padding: 30px;
margin: 10px 5px;



}


.amount{


display: flex;
justify-content: space-between ;
align-items: center;
 color: white;


}


.amount > span{


  color:   hsl(172, 67%, 45%);
font-size: 24px;
font-weight: bold;

}


.amount > p{
font-size: 14px;
}

.amount > p > span{

font-size: 12px;
color: hsl(184, 14%, 56%)

}



.label_tip{
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  gap: 8px;
  padding: 18px 38px;
  margin-bottom: 15px;
}



.custom_label{

  box-sizing: border-box;
padding: 12px;
background-color:hsl(189, 41%, 97%);
color: hsl(186, 14%, 43%);
font-size: 16px;
font-weight: bold;
border-radius: 8px;
max-width: 110px;
text-align: center;
border: none;


}

.text-input{
  position: relative;
}





.text-input > input{

width: 120px;
color:hsl(183, 100%, 15%);
font-size: 20px;
font-weight: bold;
width: 80%;
margin: 0 auto;
display: block;
background-color: hsl(189, 41%, 97%);
border:none;
text-align: right;
box-sizing: border-box;
padding: 10px;
margin-bottom: 25px;
border-radius: 5px;


}





.subtitle{

margin-left: 30px;
font-size: 14px;
margin-bottom: 10px;
/* color: hsl(184, 14%, 56%) */
/* color: hsl(186, 14%, 43%); */
color: hsl(183, 100%, 15%);
}


.input_error{
position: absolute;
right: 40px;
top:0px;
font-size: 12px;
color: hsl(0, 76%, 68%);

}


.text-input > input:focus{
  outline: 2px solid hsl(172, 67%, 45%);
}


.icon-input{

position: absolute;
left: 60px;
top: 35px;

}

@media screen and (min-width: 600px) {

.container{
  display: grid;
  grid-template-columns: 1fr 1fr;

  max-width: 70%;
  margin:0 auto;
  border-radius: 10px;
  min-height: auto;

}

.label_tip{
  grid-template-columns:  repeat(3,minmax(50px,1fr));
  grid-template-rows: 1fr 1fr 1fr;
  gap: 8px;
  padding: 18px 38px;
  margin-bottom: 15px;
}


.display{
  gap:15px;
}



.amount > span{

font-size: 32px;

}



.btn{

align-self:stretch;
max-width: none;
margin-top: auto;


}
.btn:hover{
  background-color: hsl(185, 41%, 84%);
 cursor: pointer;
}

.custom_label{
  cursor: pointer;
}


.custom_label:focus{
  outline:2px solid hsl(172, 67%, 45%);
}


}
  </style>



