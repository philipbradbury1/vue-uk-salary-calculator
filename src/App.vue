<template>
  <SalaryInput @new-salary="updateSalary"></SalaryInput>
  <StudentLoan @checked-loans="updateLoans"></StudentLoan>
  <PensionInput @pension-amount="updatePension"></PensionInput>
  <TableViewSelector @checked-views="updateViews"/>
  <Breakdown :salary="salary" :checkedViews="checkedViews" :pension="pension" :checkedLoans="checkedLoans"/>
<h3>pension app {{pension}}</h3>
</template>

<script>

import SalaryInput from './components/SalaryInput.vue';
import Breakdown from './components/BreakdownTable.vue';
import StudentLoan from './components/StudentLoan.vue';
import PensionInput from './components/PensionInput.vue';
import TableViewSelector from './components/TableViewSelector.vue';


export default {
  data(){
    return{
      salary: null,
      pension: null,
      checkedViews: [],
      checkedLoans: [],
    }
  },
  name: 'App',
  components: {
    SalaryInput,
    Breakdown,
    TableViewSelector,
    StudentLoan,
    PensionInput
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
