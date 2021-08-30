<template>


 <SalaryInput @new-salary="updateSalary"></SalaryInput>



  <div>
    <Tabs @tab-name="updateTab">
      <Tab :currentTab="currentTab" title="Tab 1"><TaxCode></TaxCode></Tab>
      <Tab :currentTab="currentTab" title="Tab 2"><StudentLoan @checked-loans="updateLoans"></StudentLoan></Tab>
      <Tab :currentTab="currentTab" title="Tab 3"><PensionInput @pension-amount="updatePension"></PensionInput></Tab>
      <Tab :currentTab="currentTab" title="Tab 4">Hello From Tab 4</Tab>
    </Tabs>
  </div>


 
  
  
  
  <TableViewSelector @checked-views="updateViews"/>
  <Breakdown :salary="salary" :checkedViews="checkedViews" :pension="pension" :checkedLoans="checkedLoans"/>
</template>

<script>


import SalaryInput from './components/SalaryInput.vue';
import TaxCode from './components/TaxCode.vue';
import StudentLoan from './components/StudentLoan.vue';
import PensionInput from './components/PensionInput.vue';
import Breakdown from './components/BreakdownTable.vue';
import TableViewSelector from './components/TableViewSelector.vue';
import Tab from './components/Tab.vue';
import Tabs from './components/Tabs.vue';


export default {
  data(){
    return{
      salary: null,
      pension: null,
      checkedViews: [],
      checkedLoans: [],
      currentTab: 'Tab 1'
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
    Tabs
  },
  methods:{
    updateSalary(salary){
      this.salary = salary;
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
