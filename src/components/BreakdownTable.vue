<template>
  <table>
    <thead>
      <tr>
        <th class="oneline">&nbsp;</th>
        <th class="cell">Gross Income</th>
        <th class="cell">Taxable Income</th>
        <th class="cell">Tax</th>
        <th class="cell">National Insurance</th>
        <th class="cell">2021 Take Home</th>
        <th class="cell">2020 Take Home</th>
      </tr>
    </thead>
    <tbody>
      <TableTr v-for="view in views" :item="view" :salary="yearlySalary" :key="view.id"></TableTr>
    </tbody>
  </table>
{{checkedLoans}}
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


import TableTr from './TableTr.vue';

export default {
  props:['salary','checkedViews', 'checkedLoans'],
  components: {
    TableTr,
  },
   data(){
      return {
        taxFree: 12570,
        studentLoan: 0,
        views:[
          {
            id: 'year123',
            name: 'Year',
            show: false,
          },
          {
            id: 'month123',
            name: 'Month',
            show: false,
          },
          {
            id: 'weekly4123',
            name: 'Weekly4',
            show: false,
          },
          {
            id: 'weekly2123',
            name: 'Weekly2',
            show: false,
          },
          {
            id: 'weekly123',
            name: 'Weekly',
            show: false,
          },
          {
            id: 'daily123',
            name: 'Daily',
            show: false,
          },
        ],
      }
   },
 
   watch:{
    checkedViews: {
      
      deep:true,
      
      handler(val){

        for (const property in val) {

          var prop = property;

          for (const view in  this.views) {

            if(prop == this.views[view].name){
              this.views[view].show = val[property]
            }
            
          }
        } 
      }
    },
     checkedLoans: {

       deep:true,

       handler(val){

        if(this.salary > 19884){

         if(val.repaymentplan1){

            Math.floor( (this.salary - 19884) / 12 * 0.09 )
           
          }
            
        }

        if(this.salary > 21000){

          if(val.postgradloan){
            Math.floor( (this.salary - 21000) / 12 * 0.06 )
          }

        }

          return this.studentLoan;
       }
    }
   },
   computed:{
     yearlySalary(){

        if(this.salary > 0){
        
          let salary = this.salary;
          let taxable = ((this.salary - this.taxFree) < 0)? 0 : this.salary - this.taxFree ;
          let tax = taxFun(salary); 
          let nI = nationalInsurance(salary);
          //let loan = this.studentLoan;
          let takeHome = salary - (tax + nI);

          return [Number(salary), taxable, tax, nI, takeHome];
          
        }
        return null
     }
    
   },
  
  

}
</script>

<style >
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

th:nth-child(even),
tr:nth-child(even),
 td:nth-child(even){
    background: rgba(0, 0, 0, .05);
}

.cell:not(:last-child) {
    border-bottom: 0;
}

.oneline {
    line-height: 48px;
}


.cell{
    line-height: 48px;
    border: 1px solid rgba(0, 0, 0, .1);
    border-left: none;
    padding: 0 8px;
    min-height: 49px;
    text-align: right;
}

th.cell {
    border-left: 1px solid rgba(0, 0, 0, .1);
    width: 168px;
    text-align: left;
}

.coloum-width{
  width:150px
}

</style>