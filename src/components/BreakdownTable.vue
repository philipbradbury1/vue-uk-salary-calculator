<template>
  <table>
    <thead>
      <tr>
        <th class="oneline">&nbsp;</th>
        <th class="cell">Gross Income</th>
        <th v-if="pensionAmount > 0" class="cell">Pension Deductions</th>
        <th class="cell">Taxable Income</th>
        <th class="cell">Tax</th>
        <th class="cell">National Insurance</th>
        <th v-if="studentLoan > 0" class="cell">Student Loan</th>
        <th class="cell">2021 Take Home</th>
        <th class="cell">2020 Take Home</th>
      </tr>
    </thead>
    <tbody>
      <TableTr v-for="view in views" :item="view" :salary="yearlySalary" :key="view.id"></TableTr>
    </tbody>
  </table>
</template>

<script>

function taxLetter(code){
  let codes = ['OT','BR','C','COT','CBR','CD0','CD1','D0','D1','L','M','N','NT','S','SOT','SBR','SD0','SD1','SD2','T'];
  let confirmedCode = codes.find(element => code.includes(element));
  return confirmedCode
}

var nationalInsurance = function(salary){
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
  props:['salary','checkedViews', 'checkedLoans', 'pension', 'taxCode' ],
  components: {
    TableTr,
  },
  data(){
    return {
      taxFree: 12570,
      studentLoan: 0,
      pensionAmount: 0,
      userTaxCode: null,
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
    taxCode: function(val){

      this.userTaxCode = val;

    },
    checkedViews: {
      
      deep:true,
      
      handler(val){

        for (const property in val) {

          var prop = property;

          for (const view in this.views) {

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
          let totalLoan = 0;
          if(this.salary > 19884 && val.repaymentplan1){
            totalLoan += Math.floor( ((this.salary - 19884) / 12).toFixed(5) * 0.09 ); 
          }
          if(this.salary > 27288 && val.repaymentplan2 && !val.repaymentplan1){
            totalLoan += Math.floor( ((this.salary - 27288) / 12).toFixed(5) * 0.09 );
          }
          if(this.salary > 21000 && val.postgradloan){
            totalLoan += Math.trunc( ((this.salary - 21000) /12 ).toFixed(5) * 0.06  );
          }
            return this.studentLoan = totalLoan;
       }
    },
    pension:function(){
        let tempSal = this.salary
        if(tempSal > 6240){
          if(tempSal > 50270){ tempSal = 50270}
          return this.pensionAmount = (tempSal - 6240) / 100 * this.pension
        }
      return this.pensionAmount = 0
    },

  },
   computed:{
     yearlySalary(){
        if(this.salary > 0){
          let salary = this.salary;
          let pension = this.pensionAmount;
          let tax = this.taxAmount(salary, this.userTaxCode); 
          let taxable = ((this.salary - this.taxFree) < 0) ? 0 : this.salary - this.taxFree;
          let nI = nationalInsurance(salary);
          let loan = this.studentLoan;
          let takeHome = salary - (tax + nI);
          return [Number(salary),pension, taxable, tax, nI, loan, takeHome];
        }
        return null
     },
     
   },
   methods:{

     taxAmount: function(salary, taxCode){

      let confirmedTaxCode = null;

      if(taxCode != null) {
        confirmedTaxCode = taxLetter(taxCode);
      }

      if(confirmedTaxCode == null  || confirmedTaxCode == 'L' ){

        let taxFreeAmount = 12570;

        if(confirmedTaxCode == "L"){
          taxFreeAmount = taxCode.replace(confirmedTaxCode,'0');
        }

        this.taxFree = taxFreeAmount
      
        if(salary <= taxFreeAmount){
          return 0
        }
        else if (salary <= 50270){
          return (salary - taxFreeAmount) * 0.20 
        }
        else if(salary <= 150000){
          return (salary - 50270) * 0.40 + 7540 
        }
        else if(salary > 150001){
          return (salary - 150000) * 0.45 + 52460
        }
      }

      if(taxCode == 'BR'){
        return salary * 0.20
      }

      if(taxCode == 'OT'){
        this.taxFree = 0;
        return salary * 0.20
      }

      return null

    }
     
   }
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
  width:200px
}

</style>