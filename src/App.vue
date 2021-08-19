<template>
  <SalaryInput @new-salary="updateSalary"></SalaryInput>
  <StudentLoan @checked-loans="updateLoans"></StudentLoan>
  <TableViewSelector @checked-views="updateViews"/>
  <Breakdown :salary="salary" :checkedViews="checkedViews"  :checkedLoans="checkedLoans"/>

</template>

<script>

import SalaryInput from './components/SalaryInput.vue';
import Breakdown from './components/BreakdownTable.vue';
import StudentLoan from './components/StudentLoan.vue';
import TableViewSelector from './components/TableViewSelector.vue';

export default {
  data(){
    return{
      salary: null,
      checkedViews: [],
      checkedLoans: [],
    }
  },
  name: 'App',
  components: {
    SalaryInput,
    Breakdown,
    TableViewSelector,
    StudentLoan
  },
  methods:{
    updateSalary(salary){
      this.salary = salary;
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
