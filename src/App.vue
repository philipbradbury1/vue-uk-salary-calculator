<template>
  <SalaryInput @new-salary="updateSalary"></SalaryInput>
  <Breakdown :salary="salary"/>
  <!-- <p> your salary is {{salary}}</p> -->
</template>

<script>

import SalaryInput from './components/SalaryInput.vue';
import Breakdown from './components/BreakdownTable.vue'

export default {
  data(){
    return{
      salary: null,
    }
  },
  name: 'App',
  components: {
    SalaryInput,
    Breakdown
    
  },
  methods:{
    updateSalary(salary){
      this.salary = salary;
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
