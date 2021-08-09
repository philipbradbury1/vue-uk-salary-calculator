<template>
  <SalaryInput @new-salary="updateSalary"></SalaryInput>
  <TableViewSelector @checked-views="updateViews"/>
  <Breakdown :salary="salary" :checkedViews="checkedViews"/>
   <!--<p> your salary is {{salary}}</p> -->
 <!-- <span>Checked names: {{ checkedViews }}</span> -->
</template>

<script>

import SalaryInput from './components/SalaryInput.vue';
import Breakdown from './components/BreakdownTable.vue';
import TableViewSelector from './components/TableViewSelector.vue';

export default {
  data(){
    return{
      salary: null,
      checkedViews: [],
    }
  },
  name: 'App',
  components: {
    SalaryInput,
    Breakdown,
    TableViewSelector
    
  },
  methods:{
    updateSalary(salary){
      this.salary = salary;
    },
    updateViews(views){
      this.checkedViews = views;

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
