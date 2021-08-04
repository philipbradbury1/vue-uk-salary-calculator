<template>
<div>
    <p> your salary is {{salary}}</p>
</div> 
 <div>{{year}}</div>
 <div>year data{{yearly}}</div>
  <table>
    <thead>
      <tr>
        <th>&nbsp;</th>
        <th>Gross Income</th>
        <th>Taxable Income</th>
        <th>Tax</th>
        <th>National Insurance</th>
        <th>2021 Take Home</th>
        <th>2020 Take Home</th>
      </tr>
    </thead>

    <tbody>
      <tr v-if="year">
        <td>Yearly</td>
        <td v-for="(data, index) in yearly" :key="`year-${index}`">
          {{data}}
        </td> 

      </tr>

       <tr v-if="month">
        <td>Month</td>
        <td>£100</td>
        <td>£100</td>
        <td>£100</td>
        <td>£100</td>
        <td>£100</td>
      </tr>
    </tbody>
  </table>
<!--
<button @click="yearly">click here</button>
<div>{{yearly()}}</div>-->

</template>

<script>
var taxFun = function(salary){

  if(salary <= 12570){
    return 0
  }
  else if (salary <= 50270){
    return (salary - 12570) * 0.20 
  }
  else if(salary <= 150000){
    return (salary - 50270) * 0.40 + 7540 
  }
  else if(salary > 150001){
    return (salary - 150000) * 0.45 + 52460
  }
}

var nationalInsurance = function(salary){
  //check first limit
    if(salary <= 9564){
      return 0
    }else if(salary <= 50268){
      return (salary - 9564) * 0.12
    }else{
      return (salary - 50268)  * 0.02  + 4884.48
    }
}

export default {
  props:['salary'],
   data(){
       return {
         taxFree: 12570,
         year: true,
         month: true,
       }
   },

   computed:{

     yearly(){
        if(this.salary > 0){
          let salary = this.salary;
          let taxable = ((this.salary - this.taxFree) < 0)? 0 : this.salary - this.taxFree ;
          let tax = taxFun(salary); 
          let nI = nationalInsurance(salary);
          let takeHome = salary - (tax + nI);
          return[salary, taxable, tax, nI, takeHome];
        }
        return null
      
     },
     monthly(){
        if(this.month){
          this.yearly().map()
        }
        return null
     },

   },
  
   
}
</script>

<style scoped>
/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type=number] {
  -moz-appearance: textfield;
}

table,
thead,
tbody{
  display: flex;
}

td,
th{
  display: block;
}

</style>