<template>

 <SalaryInput @new-salary="updateSalary"></SalaryInput>

  <div>
    <Tabs @tab-name="updateTab">
      <Tab :currentTab="currentTab" title="Tax Code"><TaxCode @tax-code="updateTaxCode"></TaxCode></Tab>
      <Tab :currentTab="currentTab" title="Student Loan"><StudentLoan @checked-loans="updateLoans"></StudentLoan></Tab>
      <Tab :currentTab="currentTab" title="Pension"><PensionInput @pension-amount="updatePension"></PensionInput></Tab>
      <Tab :currentTab="currentTab" title="Overtime"><Overtime></Overtime></Tab>
    </Tabs>
  </div>
  
  <TaxYear></TaxYear>
  <TableViewSelector @checked-views="updateViews"/>
  <Breakdown :salary="salary" :checkedViews="checkedViews" :pension="pension" :checkedLoans="checkedLoans" :taxCode="taxCode"/>
</template>

<script>


import SalaryInput from './components/SalaryInput.vue';
import TaxCode from './components/TaxCode.vue';
import StudentLoan from './components/StudentLoan.vue';
import Overtime from './components/Overtime.vue';
import PensionInput from './components/PensionInput.vue';
import Breakdown from './components/BreakdownTable.vue';
import TableViewSelector from './components/TableViewSelector.vue';
import Tab from './components/Tab.vue';
import Tabs from './components/Tabs.vue';
import TaxYear from './components/TaxYear.vue';


export default {
  data(){
    return{
      salary: null,
      taxCode: null,
      pension: null,
      checkedViews: [],
      checkedLoans: [],
      currentTab: 'Tax Code'
    }
  },
  name: 'App',
  components: {
    SalaryInput,
    TaxCode,
    Breakdown,
    TableViewSelector,
    StudentLoan,
    PensionInput,
    Tab,
    Tabs,
    Overtime,
    TaxYear
  },
  methods:{
    updateSalary(salary){
      this.salary = salary;
    },
    updateTaxCode(taxCode){
      this.taxCode = taxCode;
    },
    updatePension(pension){
      this.pension = pension;
    },
    updateViews(views){
      this.checkedViews = views;
    },
    updateLoans(loans){
      this.checkedLoans = loans; 
    },
    updateTab(tab){
      this.currentTab = tab ;
    }
  }
}
</script>

<style>

html,
body{
  margin: 0;
    background: #f2f2f2;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 80%;
  margin: 30px auto;
}

input{
  padding: 0px 8px;
  font-size: 2rem;
  width: 200px;
}

button{
  background-color: #0cb157;
  color: white;
  padding: 10px 20px;
  border: none;
  outline: none;
  cursor: pointer;
  border-radius: 5px;
}

.tab-container{
  display: flex;
}
</style>
